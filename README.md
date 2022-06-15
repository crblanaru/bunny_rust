# bunny_rust
Rust app for Bunnyshell demo


To add some data

curl --location --request POST 'env_url.domain.com/holodeck' \
--header 'Content-Type: application/json' \
--header 'Content-Type: text/plain' \
--data-raw '{
    "id": 2,
    "name": "Electric!"
}'
