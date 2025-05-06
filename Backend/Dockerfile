FROM openresty/openresty:1.27.1.2-0-alpine

# Instala o curl
RUN apk update && apk add --no-cache curl
RUN apk add --no-cache nano

# Baixa o lua-resty-jwt do GitHub
RUN curl -L https://github.com/SkyLothar/lua-resty-jwt/releases/download/v0.1.11/lua-resty-jwt-0.1.11.tar.gz | tar xvz -C /tmp \
    && mkdir -p /usr/local/openresty/site/lualib/resty/ \
    && mv /tmp/lua-resty-jwt-0.1.11/lib/resty/* /usr/local/openresty/site/lualib/resty/

# Copia o script Lua
COPY ./Backend/jwt-auth.lua /etc/nginx/jwt-auth.lua

# Copia o seu arquivo de configuração Nginx
COPY ./Backend/nginx.conf /usr/local/openresty/nginx/conf/nginx.conf

# Definir argumentos para build e variáveis de ambiente para runtime
ARG JWT_SECRET
ARG AUTH_API_URL
ARG ORDERS_API_URL
ARG DELIVERY_API_URL

# Definir valores padrão para as variáveis de ambiente
ENV AUTH_API_URL=${AUTH_API_URL:-http://auth-api:3000/}
ENV ORDERS_API_URL=${ORDERS_API_URL:-http://orders-api:3000/}
ENV DELIVERY_API_URL=${DELIVERY_API_URL:-http://delivery-api:3000/}

RUN sh -c 'echo "$(echo $JWT_SECRET)" > /etc/nginx/jwt-secret-file'
