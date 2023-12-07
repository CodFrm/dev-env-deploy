FROM debian:bookworm-slim

RUN apt-get update && apt-get install -y curl

RUN curl -sSL https://resource.fit2cloud.com/1panel/package/quick_start.sh -o quick_start.sh && \
	chmod +x quick_start.sh

CMD ./quick_start.sh