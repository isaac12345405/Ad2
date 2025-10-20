# Contratos de API - Blog Cashback Brasil

## Dados Mockados (a serem substituídos)
- **mockData.js**: 5 posts, 3 categorias, 2 comentários
- Posts estão sendo gerenciados apenas no frontend (state local)
- Newsletter apenas exibe toast sem salvar
- Comentários apenas exibem no state local

## Modelos MongoDB

### Post
```
{
  _id: ObjectId,
  title: string,
  slug: string (único, indexado),
  excerpt: string,
  content: string (HTML),
  category: string (slug da categoria),
  categoryName: string,
  author: string,
  date: string (ISO),
  readTime: string,
  image: string (URL)
}
```

### Comment
```
{
  _id: ObjectId,
  postId: string,
  author: string,
  email: string,
  content: string,
  date: string (ISO),
  approved: boolean (default: true)
}
```

### Newsletter
```
{
  _id: ObjectId,
  email: string (único),
  subscribedAt: string (ISO)
}
```

### Contact
```
{
  _id: ObjectId,
  name: string,
  email: string,
  subject: string,
  message: string,
  sentAt: string (ISO)
}
```

## Endpoints da API

### Posts
- **GET /api/posts** - Listar todos os posts
  - Response: Array<Post>
  
- **GET /api/posts/:slug** - Buscar post por slug
  - Response: Post
  
- **POST /api/posts** - Criar novo post
  - Body: { title, slug, excerpt, content, category, categoryName, image, readTime }
  - Response: Post criado
  
- **PUT /api/posts/:slug** - Atualizar post
  - Body: Campos a atualizar
  - Response: Post atualizado
  
- **DELETE /api/posts/:slug** - Deletar post
  - Response: { message: "Post deleted" }

### Comentários
- **GET /api/comments/:postId** - Listar comentários de um post
  - Response: Array<Comment>
  
- **POST /api/comments** - Criar comentário
  - Body: { postId, author, email, content }
  - Response: Comment criado

### Newsletter
- **POST /api/newsletter** - Inscrever email
  - Body: { email }
  - Response: { message: "Subscribed successfully" }

### Contato
- **POST /api/contact** - Enviar mensagem de contato
  - Body: { name, email, subject, message }
  - Response: { message: "Message sent" }

### Categorias
- **GET /api/posts/category/:slug** - Listar posts por categoria
  - Response: Array<Post>

## Integração Frontend-Backend

### Arquivos a modificar no Frontend:
1. **mockData.js** - Será substituído por chamadas à API
2. **pages/Home.jsx** - Buscar posts da API
3. **pages/PostDetail.jsx** - Buscar post e comentários da API, enviar novos comentários
4. **pages/Category.jsx** - Buscar posts por categoria da API
5. **pages/Admin.jsx** - CRUD de posts via API
6. **components/Sidebar.jsx** - Enviar email newsletter para API
7. **pages/Contato.jsx** - Enviar mensagem para API

### Estratégia de Integração:
1. Criar modelos MongoDB no backend
2. Criar todas as rotas da API
3. Popular banco com posts iniciais (seed)
4. Substituir mockData por chamadas axios no frontend
5. Testar cada fluxo individualmente
