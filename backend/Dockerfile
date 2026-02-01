FROM oven/bun:1 as base
WORKDIR /app

COPY package.json bun.lockb* ./
COPY prisma ./prisma/

RUN bun install

COPY . .

# Generate Prisma Client
RUN bun x prisma generate

FROM oven/bun:distroless
COPY --from=base /app /app
WORKDIR /app
EXPOSE 3000
CMD ["bun", "src/index.ts"]
