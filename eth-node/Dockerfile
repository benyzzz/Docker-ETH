# Utilise une image de base appropriée
FROM ubuntu:latest

# Installe les dépendances nécessaires
RUN apt-get update && apt-get install -y \
    software-properties-common \
    git \
    curl \
    build-essential \  # Installe make, gcc, et d'autres outils de compilation
RUN apt-get update && apt-get install -y software-properties-common git curl build-essential golang-go && rm -rf /var/lib/apt/lists/*

# Clone et installe Geth (noeud Ethereum)
RUN git clone https://github.com/ethereum/go-ethereum.git
WORKDIR /go-ethereum
RUN make geth

# Expose le port utilisé par le noeud Ethereum
EXPOSE 30303

# Commande par défaut pour démarrer le noeud Ethereum
CMD ["/go-ethereum/build/bin/geth", "--syncmode", "full"]