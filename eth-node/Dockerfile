# Utilise une image de base Ubuntu 22.04
FROM ubuntu:22.04

# Met à jour les paquets et installe les dépendances nécessaires
RUN apt-get update && apt-get install -y \
    software-properties-common \
    git \
    curl \
    build-essential && rm -rf /var/lib/apt/lists/*  # Installe make, gcc, et dautres outils de compilation

# Télécharge et installe Go manuellement (version 1.20)
RUN curl -OL https://go.dev/dl/go1.20.linux-amd64.tar.gz && \
    tar -C /usr/local -xzf go1.20.linux-amd64.tar.gz && \
    rm go1.20.linux-amd64.tar.gz

# Ajoute Go au PATH
ENV PATH="/usr/local/go/bin:${PATH}"

# Clone le dépôt Ethereum (Geth)
RUN git clone https://github.com/ethereum/go-ethereum.git

# Définit le répertoire de travail
WORKDIR /go-ethereum

# Compile Geth
RUN make geth

# Expose le port utilisé par le noeud Ethereum
EXPOSE 30303

# Commande par défaut pour démarrer le noeud Ethereum
CMD ["/go-ethereum/build/bin/geth", "--syncmode", "full"]