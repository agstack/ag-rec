FROM node:14.18.1 as builder

# Change working directory
WORKDIR /app

COPY . .

# Install npm packages
RUN npm install

# Production build
RUN npm run build

# Pulling new Node image to just serve the build components on serve in production
FROM node:14-alpine

# Install serve
RUN npm install -g serve

# Copy build dir from builder stage to production Node image
COPY --from=builder /app/build /app

#COPY --from=builder /app/.env /app/build

EXPOSE 4000

# Start the App via serve
CMD ["serve", "-l", "4000", "/app"]