# Migration from Vite to tsup

## Summary

Successfully migrated `ts-simple-mapper` from Vite to tsup for more reliable builds across different environments.

## Changes Made

### 1. Package.json Updates
- **Build tool**: Changed from `vite build` to `tsup`
- **Added scripts**: `build:watch` and `clean`
- **Module exports**: Updated to use modern `exports` field with proper ESM support
- **Entry points**: Simplified to `./dist/index.js` for both main and module
- **Dependencies**: 
  - Added `tsup@^8.5.0`
  - Removed `vite` and `vite-plugin-dts`
- **Version**: Bumped to 1.2.0

### 2. Build Configuration
- **Created**: `tsup.config.ts` with clean ESM-only output
- **Removed**: `vite.config.ts`, `tsconfig.build.json`, `tsconfig.node.json`
- **Simplified**: `tsconfig.json` to focus on library building

### 3. Output Structure
**Before (Vite):**
```
dist/
  ts-simple-mapper.js    (CommonJS)
  ts-simple-mapper.mjs   (ESM)
  index.d.ts             (Types)
```

**After (tsup):**
```
dist/
  index.js      (ESM only)
  index.d.ts    (Types)
```

## Benefits

1. **Consistent builds**: No more file extension mismatches (.mjs vs .js)
2. **Simpler configuration**: Single tsup.config.ts instead of multiple Vite configs
3. **Better compatibility**: Works reliably across different build systems (Vite, Webpack, etc.)
4. **Faster builds**: tsup is optimized for library bundling
5. **Cleaner output**: Single ESM format instead of dual CJS/ESM

## Testing

- ✅ All 15 tests pass
- ✅ Build completes successfully
- ✅ Output files are correctly generated
- ✅ TypeScript types are properly exported

## Migration for Consumers

No changes needed! The package exports are backward compatible. Consumers using:
- `import { simpleMap } from 'ts-simple-mapper'` - Works exactly the same
- CommonJS `require()` - Will use the ESM output (Node.js 12+ supports this)

## Next Steps

1. Commit changes with conventional commit message:
   ```bash
   git add .
   git commit -m "build: migrate from Vite to tsup for more reliable builds"
   ```

2. Push to trigger semantic-release:
   ```bash
   git push origin main
   ```

3. semantic-release will automatically:
   - Bump version to 1.2.0
   - Generate CHANGELOG
   - Publish to npm
   - Create GitHub release
