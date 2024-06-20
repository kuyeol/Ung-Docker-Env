docker run --name keycloak_unoptimized -p 8080:8080 \
-e KEYCLOAK_ADMIN=admin -e KEYCLOAK_ADMIN_PASSWORD=change_me \
-v /path/to/realm/data:/opt/keycloak/data/import \
quay.io/keycloak/keycloak:latest \
start-dev --import-realm





ssh -R 80:localhost:11434 serveo.net
