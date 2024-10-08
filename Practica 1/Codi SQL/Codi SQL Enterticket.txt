-- Crear base de dades
CREATE DATABASE EnterticketDB;
USE EnterticketDB;

-- Taula Lloc
CREATE TABLE Lloc (
    idLloc INT AUTO_INCREMENT PRIMARY KEY,
    nomRecinte VARCHAR(100) NOT NULL,
    carrer VARCHAR(255),
    ciutat VARCHAR(100),
    coordenadaLatitud DECIMAL(10, 8),
    coordenadaLongitud DECIMAL(11, 8)
);

-- Taula UsuariNoRegistrat
CREATE TABLE UsuariNoRegistrat (
    idUsuari INT PRIMARY KEY,
    nom VARCHAR(100) NOT NULL,
    cognoms VARCHAR(100) NOT NULL,
    email VARCHAR(255) NOT NULL,
    codiPostal VARCHAR(20) NOT NULL,
    telefon INT NOT NULL,
    eliminarUsuari BOOLEAN DEFAULT FALSE
);

-- Taula UsuariRegistrat
CREATE TABLE UsuariRegistrat (
    idUsuari INT PRIMARY KEY,
    nom VARCHAR(100) NOT NULL,
    cognoms VARCHAR(100) NOT NULL,
    email VARCHAR(255) NOT NULL,
    codiPostal VARCHAR(20) NOT NULL,
    telefon INT NOT NULL,
    contrasenya VARCHAR(255) NOT NULL,
    dataNaixament DATE NOT NULL
);

-- Taula PagamentTargetaBancaria
CREATE TABLE PagamentTargetaBancaria (
    codiReferencia VARCHAR(25) PRIMARY KEY,
    nomCompletTitular VARCHAR(255) NOT NULL,
    numeroTargeta VARCHAR(20) NOT NULL,
    numeroSecret VARCHAR(4) NOT NULL,
    dataDeVenciment DATE NOT NULL
);

-- Tabla PagamentPayPal
CREATE TABLE PagamentPayPal (
    codiReferencia VARCHAR(25) PRIMARY KEY,
    emailPayPal VARCHAR(255) NOT NULL
);

-- Taula Esdeveniment
CREATE TABLE Esdeveniment (
    idEsdeveniment INT AUTO_INCREMENT PRIMARY KEY,
    imatge BLOB,
    titolEsdeveniment VARCHAR(100) NOT NULL,
    descripcioEsdeveniment TEXT,
    data DATE NOT NULL,
    hora TIME NOT NULL,
    tipusEsdeveniment VARCHAR(100),
    idLloc INT NOT NULL,
    FOREIGN KEY (idLloc) REFERENCES Lloc(idLloc) ON DELETE CASCADE
);

-- Taula TipusEntrada
CREATE TABLE TipusEntrada (
    idTipusEntrada INT AUTO_INCREMENT PRIMARY KEY,
    preuEntrada DECIMAL(10, 2) NOT NULL,
    titolEntrada VARCHAR(100) NOT NULL,
    descripcioEntrada TEXT,
    despesaDeGestio DECIMAL(10, 2),
    entradesTotals INT NOT NULL,
    entradesSeleccionables INT NOT NULL,
    idEsdeveniment INT NOT NULL,
    FOREIGN KEY (idEsdeveniment) REFERENCES Esdeveniment(idEsdeveniment) ON DELETE CASCADE
);

-- Taula Complement
CREATE TABLE Complement (
    idComplement INT AUTO_INCREMENT PRIMARY KEY,
    titolComplement VARCHAR(255) NOT NULL,
    descripcioComplement TEXT,
    preuComplement DECIMAL(10, 2) NOT NULL,
    despesaDeGestio DECIMAL(10, 2),
    idTipusEntrada INT NOT NULL,
    FOREIGN KEY (idTipusEntrada) REFERENCES TipusEntrada(idTipusEntrada) ON DELETE CASCADE
);

-- Taula Reserva
CREATE TABLE Reserva (
    codiReserva VARCHAR(15) PRIMARY KEY,
    dataDeCompra DATE NOT NULL,
    doblersTotals DECIMAL(10, 2) NOT NULL,
    dataDePagament DATE,
    idUsuariNoRegistrat INT,
    idUsuariRegistrat INT,
    codiReferenciaTargeta VARCHAR(25),
    codiReferenciaPayPal VARCHAR(25),
    FOREIGN KEY (idUsuariNoRegistrat) REFERENCES UsuariNoRegistrat(idUsuari) ON DELETE SET NULL,
    FOREIGN KEY (idUsuariRegistrat) REFERENCES UsuariRegistrat(idUsuari) ON DELETE SET NULL,
    FOREIGN KEY (codiReferenciaTargeta) REFERENCES PagamentTargetaBancaria(codiReferencia) ON DELETE SET NULL,
    FOREIGN KEY (codiReferenciaPayPal) REFERENCES PagamentPayPal(codiReferencia) ON DELETE SET NULL
);

-- Taula Entrada
CREATE TABLE Entrada (
    codiEntrada VARCHAR(15) PRIMARY KEY,
    qr BLOB,
    escanejada BOOLEAN DEFAULT FALSE,
    numeroSeient INT,
    idTipusEntrada INT NOT NULL,
    idUsuariNoRegistrat INT,
    idUsuariRegistrat INT,
    codiReserva VARCHAR(15) NOT NULL,
    FOREIGN KEY (idTipusEntrada) REFERENCES TipusEntrada(idTipusEntrada) ON DELETE CASCADE,
    FOREIGN KEY (idUsuariNoRegistrat) REFERENCES UsuariNoRegistrat(idUsuari) ON DELETE SET NULL,
    FOREIGN KEY (idUsuariRegistrat) REFERENCES UsuariRegistrat(idUsuari) ON DELETE SET NULL,
    FOREIGN KEY (codiReserva) REFERENCES Reserva(codiReserva) ON DELETE CASCADE
);
