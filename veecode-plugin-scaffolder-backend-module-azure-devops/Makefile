PHONY: build-plugin build-plugin-dynamic build-plugin-dynamic-clean publish-plugin-dynamic publish-plugin-dynamic-local

# Build the plugin (static only)
build-plugin:
	yarn install && yarn tsc && yarn build

# Build the dynamic plugin module
build-plugin-dynamic: build-plugin
	yarn export-dynamic

build-plugin-dynamic-clean:
	yarn export-dynamic:clean

# Publish dynamic plugin
publish-plugin-dynamic: build-plugin-dynamic
	cd dist-dynamic && \
	npm publish

# Publish dynamic plugin to local registry
publish-plugin-dynamic-local: build-plugin-dynamic
	cd dist-dynamic && \
	npm publish --registry http://localhost:4873

unpublish-plugin-dynamic-local:
	cd dist-dynamic && \
	npm unpublish --registry http://localhost:4873 --force @veecode/plugin-scaffolder-backend-module-azure-devops-dynamic
