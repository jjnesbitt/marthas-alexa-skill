BUILD_PATH=./build
BABELRC=./.babelrc
WEBPACK_CONFIG=./webpack.config.js
ZIP_FILE=index.zip
LAMBDA_FUNCTION_NAME=marthas-flavor-skill

main:
	rm -rf $(BUILD_PATH) && \
	npx babel --config-file $(BABELRC) -d $(BUILD_PATH) --ignore $(WEBPACK_CONFIG) *.js && \
	cp ./package* $(BUILD_PATH)/ && \
	cd $(BUILD_PATH) && \
	npm install --only=production && \
	zip -r $(ZIP_FILE) package* *.js node_modules

push:
	aws lambda update-function-code \
		--function-name $(LAMBDA_FUNCTION_NAME) \
		--zip-file fileb://$(BUILD_PATH)/$(ZIP_FILE)

clean:
	rm -rf $(BUILD_PATH)
