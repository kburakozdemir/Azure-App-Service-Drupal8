# Testing

docker login drupal9registry.azurecr.io --username drupal9registry

docker build -t abcazure:latest \
 --build-arg GIT_TOKEN=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 \
 --build-arg BRANCH=master \
 --build-arg GIT_REPO=kburakozdemir/test-drupal-no-composer \
 .

docker run -it -p 8200:8080 abcazure:latest

docker tag abcazure:latest drupal9registry.azurecr.io/abcazure:latest

docker push drupal9registry.azurecr.io/abcazure:latest

az webapp delete --name abcazurex --resource-group kbo

az webapp create --resource-group kbo --plan phpAppPlan --name abcazurey --deployment-container-image-name drupal9registry.azurecr.io/abcazure:latest

az webapp config appsettings set --resource-group kbo --name abcazurey --settings WEBSITES_ENABLE_APP_SERVICE_STORAGE=true

az webapp config appsettings set --resource-group kbo --name abcazurey --settings WEBSITES_PORT=8080

az webapp delete --name abcazurey --resource-group kbo

az webapp create --resource-group kbo --plan phpAppPlan --name abcazurez --deployment-container-image-name drupal9registry.azurecr.io/abcazure:latest

az webapp config appsettings set --resource-group kbo --name abcazurez --settings WEBSITES_ENABLE_APP_SERVICE_STORAGE=true

az webapp config appsettings set --resource-group kbo --name abcazurez --settings WEBSITES_PORT=8080

---- yeni

docker build -t newcomposerimage:latest \
 --build-arg GIT_TOKEN=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 \
 --build-arg BRANCH=drush3 \
 --build-arg GIT_REPO=kburakozdemir/test-drupal-composer \
 .

docker run -it -p 8200:8080 newcomposerimage:latest

docker tag abcazure:latest drupal9registry.azurecr.io/newcomposerimage:latest

docker push drupal9registry.azurecr.io/newcomposerimage:latest

az webapp delete --name abcazurezcomptest --resource-group kbo
