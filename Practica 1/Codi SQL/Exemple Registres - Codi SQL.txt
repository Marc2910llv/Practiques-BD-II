INSERT INTO Lloc (nomRecinte, carrer, ciutat, coordenadaLatitud, coordenadaLongitud)
VALUES
('Palau Sant Jordi', 'Passeig Olímpic, 5-7', 'Barcelona', 41.363457, 2.151953),
('WiZink Center', 'Av. Felipe II, S/N', 'Madrid', 40.423705, -3.671841),
('Auditori Nacional', 'Carrer de Cristóbal Colón, 1', 'Andorra la Vella', 42.511285, 1.531328);

INSERT INTO UsuariNoRegistrat (idUsuari, nom, cognoms, email, codiPostal, telefon)
VALUES
(1, 'Carlos', 'García Fernández', 'cgarcia@example.com', '08001', 678123456),
(2, 'Lucía', 'Martínez López', 'lucia.martinez@example.com', '28012', 661789456),
(3, 'Miguel', 'Pérez Sánchez', 'miguel.perez@example.com', '50008', 645987321);

INSERT INTO UsuariRegistrat (idUsuari, nom, cognoms, email, codiPostal, telefon, contrasenya, dataNaixament)
VALUES
(1, 'Ana', 'López Martínez', 'ana.lopez@example.com', '08002', 612345678, 'password123', '1990-05-14'),
(2, 'Javier', 'Rodríguez Sánchez', 'javier.rodriguez@example.com', '28013', 689765432, 'password456', '1985-09-23'),
(3, 'María', 'Gómez Fernández', 'maria.gomez@example.com', '41010', 600987654, 'password789', '1992-12-10');

INSERT INTO PagamentTargetaBancaria (codiReferencia, nomCompletTitular, numeroTargeta, numeroSecret, dataDeVenciment)
VALUES
('TARJETA001', 'Ana López Martínez', '1234567812345678', '123', '2025-05-01'),
('TARJETA002', 'Javier Rodríguez Sánchez', '8765432187654321', '456', '2024-10-15'),
('TARJETA003', 'María Gómez Fernández', '4321876543218765', '789', '2026-02-28');

INSERT INTO PagamentPayPal (codiReferencia, emailPayPal)
VALUES
('PAYPAL001', 'ana.lopez.paypal@example.com'),
('PAYPAL002', 'javier.rodriguez.paypal@example.com'),
('PAYPAL003', 'maria.gomez.paypal@example.com');

INSERT INTO Esdeveniment (titolEsdeveniment, descripcioEsdeveniment, data, hora, tipusEsdeveniment, idLloc)
VALUES
('Concierto Rock', 'Un concierto de rock en vivo', '2024-11-20', '21:00:00', 'Concierto', 1),
('Partido de Baloncesto', 'Final de la liga de baloncesto', '2024-12-15', '19:00:00', 'Deporte', 2),
('Opera en directo', 'Representación de La Traviata', '2025-01-10', '20:30:00', 'Ópera', 3);

INSERT INTO TipusEntrada (preuEntrada, titolEntrada, descripcioEntrada, despesaDeGestio, entradesTotals, entradesSeleccionables, idEsdeveniment)
VALUES
(50.00, 'Entrada General', 'Acceso general al concierto', 5.00, 500, 300, 1),
(75.00, 'Entrada VIP', 'Acceso VIP con asientos preferentes', 7.50, 200, 100, 1),
(20.00, 'Entrada Normal', 'Asiento general para el partido', 2.00, 1000, 800, 2);

INSERT INTO Complement (titolComplement, descripcioComplement, preuComplement, despesaDeGestio, idTipusEntrada)
VALUES
('Camiseta Concierto', 'Camiseta exclusiva del concierto de rock', 20.00, 2.00, 1),
('Comida VIP', 'Acceso a buffet VIP', 30.00, 3.00, 2),
('Bebida', 'Vale para una bebida', 5.00, 0.50, 3);

INSERT INTO Reserva (codiReserva, dataDeCompra, doblersTotals, dataDePagament, idUsuariNoRegistrat, idUsuariRegistrat, codiReferenciaTargeta, codiReferenciaPayPal)
VALUES
('RESERVA001', '2024-10-01', 55.00, '2024-10-01', 1, NULL, 'TARJETA001', NULL),
('RESERVA002', '2024-10-05', 82.50, '2024-10-05', NULL, 2, NULL, 'PAYPAL002'),
('RESERVA003', '2024-11-01', 105.00, '2024-11-01', 2, NULL, 'TARJETA003', NULL);

INSERT INTO Entrada (codiEntrada, escanejada, numeroSeient, idTipusEntrada, idUsuariNoRegistrat, idUsuariRegistrat, codiReserva)
VALUES
('ENTRADA001', FALSE, 12, 1, 1, NULL, 'RESERVA001'),
('ENTRADA002', FALSE, 5, 2, NULL, 2, 'RESERVA002'),
('ENTRADA003', TRUE, 25, 3, 2, NULL, 'RESERVA003');
