# SvelteKit Adapter AWS

This project contains a SvelteKit adapter to deploy SvelteKit to AWS using AWS-CDK.

## Recent Updates (2025)

This repository has been modernized with:
- ✅ Updated AWS CDK from 2.66.0 to 2.114.1
- ✅ Updated TypeScript from 4.9.5 to 5.3.3
- ✅ Updated Node.js runtime from 16 to 20
- ✅ Updated SvelteKit to latest compatible version
- ✅ Updated all dependencies to 2025 versions
- ✅ Added working example application in `example/` directory
- ✅ Comprehensive deployment documentation

## Quick Start

See the [example/](./example/) directory for a complete working example, or follow [DEPLOYMENT.md](./DEPLOYMENT.md) for step-by-step deployment instructions.

## How to use?

1. Create a SvelteKit project "my-app" - `npm create svelte@latest my-app`
2. `cd my-app`
3. `npm install`
4. `npm install -D sveltekit-adapter-aws`
5. edit **svelte.config.js**

## Basic setup example

**svelte.config.js**

```javascript
import { adapter } from 'sveltekit-adapter-aws';
import preprocess from 'svelte-preprocess';

export default {
  preprocess: preprocess(),
  kit: {
    adapter: adapter({
      autoDeploy: true,
    }),
  },
};
```

## Architecture

![Architecture](architecture.png)

## Configuration

```typescript
export interface AWSAdapterProps {
  cdkProjectPath?: string; // AWS-CDK App file path for AWS-CDK custom deployment applications (e.g. ${process.cwd()}/deploy.js)
  artifactPath?: string; // Build output directory (default: build)
  autoDeploy?: boolean; // Should automatically deploy in SvelteKit build step (default: false)
  stackName?: string; // AWS-CDK CloudFormation Stackname (default: AWSAdapterStack-Default)
  esbuildOptions?: any; // Override or extend default esbuild options. Supports `external` (default `['node:*']`), `format` (default `cjs`), `target` (default `node20`), `banner` (default `{}`).
  FQDN?: string; // Full qualified domain name of CloudFront deployment (e.g. demo.example.com)
  MEMORY_SIZE?: number; // Memory size of SSR lambda in MB (default 128 MB)
  LOG_RETENTION_DAYS?: number; // Log retention in days of SSR lambda (default 7 days)
  zoneName?: string; // The name of the hosted zone in Route 53 (defaults to the TLD from the FQDN)
}
```

## Working Example

A complete working example is available in the `example/` directory. It demonstrates:
- SvelteKit application with SSR
- API routes running on Lambda
- Static asset optimization
- AWS deployment configuration

To run the example:
```bash
cd example
npm install
npm run build
```

See [example/README.md](./example/README.md) for detailed instructions.

## Example usages

- [Basic](https://github.com/MikeBild/sveltekit-adapter-aws-basic-example)
- [Advanced](https://github.com/MikeBild/sveltekit-adapter-aws-advanced-example)
- [Full Workshop Example](https://github.com/MikeBild/serverless-workshop-sveltekit)
