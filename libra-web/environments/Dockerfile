FROM node:22-bookworm as builder
WORKDIR /app
RUN npm i -g bun
COPY package.json bun.lockb .
RUN bun i --frozen-lockfile
COPY . .
RUN bun build --outfile=bundle.js --outdir ./dist ./src/my-element.ts

FROM nginx:1.26.2-alpine
COPY --from=builder /app/dist /user/share/nginx/html
CMD ["nginx", "-g", "daemon off;"]