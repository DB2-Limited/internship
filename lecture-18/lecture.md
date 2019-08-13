# Lecture 18

### HTML -> PDF

- https://github.com/devongovett/node-wkhtmltopdf
- https://github.com/foliojs/pdfkit


### Swagger

```yaml
post:
  summary: Sign In
  description: Sign iin user and return user object with JWT token
  tags:
    - Accounts
  security:
    - ApiKeyAuth: []
  requestBody:
    content:
      application/json:
        schema:
          type: object
          properties:
            email:
              type: string
            password:
              type: string
  responses:
    "200":
      content:
        application/json:
          description: User object with JWT token
          schema:
            type: object
            properties:
              user:
                type: object
                properties:
                  fullName:
                    type: string
                    description: Full name of user
                  photo:
                    type: string
                    description: URL for user photo
              token:
                type: string
                description: JWT token for this user
    default:
      $ref: "../../models/error.yml"

```

```yaml
openapi: 3.0.0
info:
  title: My Fixer API docs
  description: Made with ❤️️️️
  version: 0.0.1
  host: localhost:3000
tags:
  - name: Accounts
paths:
  /accounts/sign-in:
    $ref: methods/accounts/signIn.yml
servers:
  - url: /api
components:
  securitySchemes:
    ApiKeyAuth:
      type: apiKey
      in: header
      name: Authorization
# security:
#   - ApiKeyAuth: []
```

```js
app.use(serve('docs'));
app.use(koaSwagger({
  routePrefix: '/docs',
  hideTopbar: true,
  swaggerOptions: {
    url: 'http://localhost:3000/docs.yml',
  },
}));
```

```js
exports.testPdf = async (ctx) => {
  // const html = '<span>Hello world!</span>';
  const html = await nunjucks.render(path.join(__dirname, '../templates/invoice.html'), {
    name: 'Vasya Pupkin',
  });
  // console.log(html);

  // await wkhtmltopdf(html).pipe(fs.createWriteStream('out.pdf'));
  // await wkhtmltopdf(html, {
  //   output: 'qwe.pdf',
  // });
  // ctx.body = {
  //   success: true,
  // };
  ctx.set('Content-Type', 'application/pdf');
  // ctx.attachment('invoice.pdf');
  ctx.body = await wkhtmltopdf(html);
};
```