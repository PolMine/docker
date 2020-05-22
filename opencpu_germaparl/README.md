docker build \
  --build-arg AWS_ACCESS_KEY_ID=$(grep "aws_access_key_id" ~/.aws/credentials | awk '{print $3}') \
  --build-arg AWS_SECRET_ACCESS_KEY=$(grep "aws_secret_access_key" ~/.aws/credentials | awk '{print $3}') \
  --tag opencpu_germaparl:latest \
  opencpu_germaparl
