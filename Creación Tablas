
SET AUTOCOMMIT on;
SET SERVEROUTPUT on;

 

DROP VIEW Vista_Puntos;
DROP VIEW Patrocinios_Temporada;

DROP INDEX Tipo_Pieza;
DROP INDEX Fecha_Factura;


DROP TABLE PatrocinadorPatrocinaEquipo;
DROP TABLE MotoParticipaMotoGP;
DROP TABLE CocheParticipaF2;
DROP TABLE CocheParticipaF1;
DROP TABLE VehiculoParticipaCircuito;
DROP TABLE PilotoTieneMecanico;
DROP TABLE PilotoCompiteCircuito;
DROP TABLE PilotoConduceVehiculo;
DROP TABLE EntrenamientoCarrera ;
DROP TABLE JefeEquipo ;
DROP TABLE MotoGP ;
DROP TABLE F2 ;
DROP TABLE F1 ;
DROP TABLE Contrato ;
DROP TABLE Pieza ;
DROP TABLE Factura ;
DROP TABLE Contable ;
DROP TABLE Proveedor ;
DROP TABLE OperadorProduccion ;
DROP TABLE Carrera ;
DROP TABLE Entrenamiento ;
DROP TABLE Calendario ;
DROP TABLE Circuito ;
DROP TABLE Moto;
DROP TABLE Coche ;
DROP TABLE Vehiculo ;
DROP TABLE IngenieroCarrera ;
DROP TABLE Mecanico ;
DROP TABLE Piloto ;
DROP TABLE Patrocinador ;
DROP TABLE Empleado ;
DROP TABLE Equipo ;


CREATE TABLE Empleado (
   EmpleadoID int not null PRIMARY KEY,
    Nombre varchar(255),
    Apellidos varchar(255),
    DNI varchar(20) UNIQUE,
    EquipoID int,
    SuperiorID int,
    Telefono varchar(15),
    CHECK (EmpleadoID > 0)
);
 ALTER TABLE Empleado ADD FOREIGN KEY  (SuperiorID) REFERENCES Empleado(EmpleadoID) ON DELETE SET NULL;




CREATE TABLE Equipo (
     EquipoID int PRIMARY KEY,
     NumIntegrantes int,
     JefeEquipoID int,
     FechaCreacion DATE,
     NombreEquipo varchar(255)
);
 ALTER TABLE Empleado ADD FOREIGN KEY  (EquipoID) REFERENCES Equipo(EquipoID) ON DELETE CASCADE;



CREATE TABLE Patrocinador (
    PatrocinadorID int PRIMARY KEY,
    Nombre varchar(255),
    ValorMonetario float,
    CHECK (ValorMonetario > 0)
);


CREATE TABLE Piloto (
    EmpleadoID int PRIMARY KEY,
    Superlicencia varchar(50),
    EquipoID int,
    SustitutoID int,
    IdIngeniero int,
    FOREIGN KEY (EmpleadoID) REFERENCES Empleado(EmpleadoID),
    FOREIGN KEY (EquipoID) REFERENCES Equipo(EquipoID)
);

 ALTER TABLE Piloto ADD FOREIGN KEY  (SustitutoID) REFERENCES Piloto(EmpleadoID) ON DELETE SET NULL;



CREATE TABLE Mecanico (
    EmpleadoID int PRIMARY KEY,
    PosicionBoxes varchar(50),
    EquipoID int,
    FOREIGN KEY (EmpleadoID) REFERENCES Empleado(EmpleadoID),
    FOREIGN KEY (EquipoID) REFERENCES Equipo(EquipoID)
);


CREATE TABLE IngenieroCarrera (
    EmpleadoID int PRIMARY KEY,
    PilotoID int,
    EquipoID int,
    DirigidoPor int,  
    Especialidad varchar(100),  
    FOREIGN KEY (EmpleadoID) REFERENCES Empleado(EmpleadoID),
    FOREIGN KEY (PilotoID) REFERENCES Piloto(EmpleadoID),
    FOREIGN KEY (EquipoID) REFERENCES Equipo(EquipoID)
   
);


CREATE TABLE Vehiculo (
    VehiculoID int PRIMARY KEY,
    Dimensiones varchar(255),
    AñoFabricacion int,
    VelMax int,
    NumeroBastidor varchar(255),
    Color varchar(100),
    TipoRueda varchar(100)
    
);

CREATE TABLE Coche (
    VehiculoID int PRIMARY KEY,
    CocheID int,
    ConfigMotor varchar(255),
    Aerodinamica varchar(255),
    Transmision varchar(255),
   
    FOREIGN KEY (VehiculoID) REFERENCES Vehiculo(VehiculoID)
);

CREATE TABLE Moto (
    VehiculoID int PRIMARY KEY,
    MotoID int,
    AlturaAsiento float,
    TipoManillar varchar(60),
    CilindradaCC int,
    FOREIGN KEY (VehiculoID) REFERENCES Vehiculo(VehiculoID)
);


CREATE TABLE Circuito (
    CircuitoID int PRIMARY KEY,
    Nombre varchar(255),
    NumeroCurvas int,
    SentidoGiro varchar(50),
    Pais varchar(30),
    Ciudad varchar(100)
);

CREATE TABLE Calendario (
    Temporada int,
    Fecha date,
    CircuitoID int,
    VehiculoID int,
    PilotoID int,
    EquipoID int,
   
    PRIMARY KEY (CircuitoID, VehiculoID, PilotoID, EquipoID, Fecha),
    FOREIGN KEY (CircuitoID) REFERENCES Circuito(CircuitoID) ON DELETE CASCADE,
    FOREIGN KEY (VehiculoID) REFERENCES Vehiculo(VehiculoID) ON DELETE CASCADE,
    FOREIGN KEY (PilotoID) REFERENCES Piloto(EmpleadoID) ON DELETE CASCADE,
    FOREIGN KEY (EquipoID) REFERENCES Equipo(EquipoID) ON DELETE CASCADE
   
);


CREATE TABLE Entrenamiento (
    EntrenamientoID int,
    EquipoID int,
    Rendimiento float,
    MejoraTiempo decimal(8, 3),
    PRIMARY KEY (EquipoID, EntrenamientoID),
    FOREIGN KEY (EquipoID) REFERENCES Equipo(EquipoID) ON DELETE CASCADE,
    CHECK (Rendimiento >= 0 AND Rendimiento <= 100)
);



CREATE TABLE Carrera (
    CarreraID int,
    PilotoID int,
    CircuitoID int,
    VehiculoID int,
    NumeroEntradasBoxes int,
    Accidente int,
    NumVueltas int,
    Tiempo varchar(100),
    Puntos int,
    PRIMARY KEY (VehiculoID, PilotoID, CircuitoID),
    FOREIGN KEY (VehiculoID) REFERENCES Vehiculo(VehiculoID),
    FOREIGN KEY (PilotoID) REFERENCES Piloto(EmpleadoID),
    FOREIGN KEY (CircuitoID) REFERENCES Circuito(CircuitoID)
);

CREATE TABLE Proveedor (
    ProveedorID int PRIMARY KEY,
    Nombre varchar(255)
   
);

CREATE TABLE Pieza (
    PiezaID int PRIMARY KEY,
    NumeroSerie varchar(255),
    Precio decimal(10, 2),
    Stock int,
    Dimensiones varchar(100),
    FechaVenta int,
    Tipo varchar(100),
    ProveedorID int,
    VehiculoID int,
    FacturaID int,
    OperadorID int,

    FOREIGN KEY (ProveedorID) REFERENCES Proveedor(ProveedorID),
    FOREIGN KEY (VehiculoID) REFERENCES Vehiculo(VehiculoID)
 );
 


CREATE TABLE Contable (
    EmpleadoID int PRIMARY KEY,
    NumDespacho int,
    FOREIGN KEY (EmpleadoID) REFERENCES Empleado(EmpleadoID)

);

CREATE TABLE Factura (
    FacturaID int PRIMARY KEY,
    NumPiezas int,
    Fechas DATE,
    ContableID int,
    FOREIGN KEY (ContableID) REFERENCES Contable(EmpleadoID) on DELETE CASCADE,
    CHECK (NumPiezas > 0)
);

 ALTER TABLE Pieza ADD FOREIGN KEY  (FacturaID) REFERENCES Factura(FacturaID) on DELETE SET NULL;

CREATE TABLE Contrato (
        ContratoID int PRIMARY KEY,
        EmpleadoID int,
        FechaInicio DATE,
        FechaFin DATE,
        Descripcion varchar(500),
        Salario int,
   
FOREIGN KEY (EmpleadoID) REFERENCES Empleado(EmpleadoID),

CHECK (FechaInicio < FechaFin)
);

CREATE TABLE OperadorProduccion (
    EmpleadoID int PRIMARY KEY,
    FOREIGN KEY (EmpleadoID) REFERENCES Empleado(EmpleadoID)
);
 ALTER TABLE Pieza ADD FOREIGN KEY  (OperadorID) REFERENCES OperadorProduccion(EmpleadoID) on DELETE SET NULL;

CREATE TABLE F1 (
    F1ID int  PRIMARY KEY,
    Descripcion varchar(100),
    FOREIGN KEY (F1ID) REFERENCES Equipo(EquipoID)
);
CREATE TABLE F2 (
    F2ID int,
    Descripcion varchar(100),
    FOREIGN KEY (F2ID) REFERENCES Equipo(EquipoID)

);
CREATE TABLE MotoGP (
    MotoGPID int PRIMARY KEY,
    Descripcion varchar(100),
    FOREIGN KEY (MotoGPID) REFERENCES Equipo(EquipoID)

);

CREATE TABLE JefeEquipo (
    EmpleadoID int PRIMARY KEY,
    FOREIGN KEY (EmpleadoID) REFERENCES Empleado(EmpleadoID)
);

CREATE TABLE EntrenamientoCarrera (
    VehiculoID int,
    CircuitoID int,
    PilotoID int,
    EntrenamientoID int,
    EquipoID int,
    fecha DATE,
    PRIMARY KEY (VehiculoID ,CircuitoID,PilotoID,EntrenamientoID,EquipoID ),    
    FOREIGN KEY (PilotoID) REFERENCES Piloto(EmpleadoID) ON DELETE CASCADE,
    FOREIGN KEY (CircuitoID) REFERENCES Circuito(CircuitoID) ON DELETE CASCADE,
    FOREIGN KEY (EquipoID,EntrenamientoID) REFERENCES Entrenamiento ON DELETE CASCADE

);

CREATE TABLE PilotoConduceVehiculo(
    PilotoID int,
    VehiculoID int,
    PRIMARY KEY (PilotoID,VehiculoID),
    FOREIGN KEY (PilotoID) REFERENCES Piloto(EmpleadoID) ON DELETE CASCADE,
    FOREIGN KEY (VehiculoID) REFERENCES Vehiculo(VehiculoID) ON DELETE CASCADE
   
);


CREATE TABLE PilotoCompiteCircuito(
    PilotoID int,
    CircuitoID int,
    PRIMARY KEY (PilotoID,CircuitoID),
    FOREIGN KEY (PilotoID) REFERENCES Piloto(EmpleadoID) ON DELETE CASCADE,
    FOREIGN KEY (CircuitoID) REFERENCES Circuito(CircuitoID) ON DELETE CASCADE

);


CREATE TABLE PilotoTieneMecanico(
    PilotoID int,
    MecanicoID int,
    PRIMARY KEY (PilotoID,MecanicoID),
    FOREIGN KEY (PilotoID) REFERENCES Piloto(EmpleadoID) ON DELETE CASCADE,
    FOREIGN KEY (MecanicoID) REFERENCES Mecanico(EmpleadoID) ON DELETE CASCADE

);

CREATE TABLE VehiculoParticipaCircuito(
    VehiculoID int,
    CircuitoID int,
    PRIMARY KEY (VehiculoID ,CircuitoID ),
    FOREIGN KEY (VehiculoID ) REFERENCES Vehiculo(VehiculoID) ON DELETE CASCADE,
    FOREIGN KEY (CircuitoID ) REFERENCES Circuito(CircuitoID) ON DELETE CASCADE
);


CREATE TABLE CocheParticipaF1(
    CocheID int,
    F1ID int,
   
PRIMARY KEY (CocheID  ,F1ID  ),
    FOREIGN KEY (CocheID) REFERENCES Coche(VehiculoID) ON DELETE CASCADE,
    FOREIGN KEY (F1ID) REFERENCES F1(F1ID) ON DELETE CASCADE
);

CREATE TABLE CocheParticipaF2(
    CocheID int,
    F2ID INT,

    PRIMARY KEY (CocheID,F2ID),
    FOREIGN KEY (CocheID) REFERENCES Coche(VehiculoID) ON DELETE   CASCADE,
    FOREIGN KEY (F2ID) REFERENCES Equipo(EquipoID) ON DELETE CASCADE


);


CREATE TABLE MotoParticipaMotoGP(
    MotoID int,
    MotoGPID int,

PRIMARY KEY (MotoID  ,MotoGPID),
    FOREIGN KEY (MotoID) REFERENCES Moto(VehiculoID) ON DELETE CASCADE,
    FOREIGN KEY (MotoGPID) REFERENCES MotoGP(MotoGPID) ON DELETE CASCADE


);


CREATE TABLE PatrocinadorPatrocinaEquipo(
    PatrocinadorID int,
    EquipoID int,
    Temporada varchar(30),

    PRIMARY KEY (PatrocinadorID,EquipoID),
    FOREIGN KEY (PatrocinadorID) REFERENCES Patrocinador(PatrocinadorID) ON DELETE CASCADE,
    FOREIGN KEY (EquipoID) REFERENCES Equipo(EquipoID) ON DELETE CASCADE
);



CREATE INDEX Fecha_Factura ON Factura(Fechas);

CREATE INDEX Tipo_Pieza ON Pieza(Tipo);


CREATE OR REPLACE VIEW Vista_Puntos (Piloto, Puntos_Totales) AS SELECT E.Nombre,SUM(Puntos) FROM Piloto P inner join Empleado E on P.EmpleadoID = E.EmpleadoID inner join Carrera C on C.PilotoID = P.EmpleadoID GROUP BY E.Nombre;

create or replace view Patrocinios_Temporada (Temporada,Num_Equipo,Num_Patrocinador,Inversion) AS SELECT pp.temporada,pp.EquipoID,p.patrocinadorID,p.valormonetario FROM Patrocinador P inner join PatrocinadorPatrocinaEquipo pp on p.PatrocinadorID= pp.patrocinadorID order by pp.temporada;

INSERT INTO Empleado (EmpleadoID, Nombre, Apellidos, DNI,  Telefono) VALUES (1, 'Lewis', 'Hamilton', 'DNI001', '123-456-7890');

INSERT INTO Empleado (EmpleadoID, Nombre, Apellidos, DNI, EquipoID, SuperiorID, Telefono)
VALUES (2, 'Max', 'Verstappen', 'DNI002', NULL, NULL, '234-567-8901');

INSERT INTO Empleado (EmpleadoID, Nombre, Apellidos, DNI, EquipoID, SuperiorID, Telefono)
VALUES (3, 'Charles', 'Leclerc', 'DNI003', NULL, NULL, '345-678-9012');

INSERT INTO Empleado (EmpleadoID, Nombre, Apellidos, DNI, EquipoID, SuperiorID, Telefono)
VALUES (4, 'Toto', 'Wolff', 'DNI004', NULL, NULL, '456-789-0123');

INSERT INTO Empleado (EmpleadoID, Nombre, Apellidos, DNI, EquipoID, SuperiorID, Telefono)
VALUES (5, 'Christian', 'Horner', 'DNI005', NULL, NULL, '567-890-1234');

INSERT INTO Empleado (EmpleadoID, Nombre, Apellidos, DNI, EquipoID, SuperiorID, Telefono)
VALUES (6, 'Mattia', 'Binotto', 'DNI006', NULL, NULL, '678-901-2345');

INSERT INTO Empleado (EmpleadoID, Nombre, Apellidos, DNI, EquipoID, SuperiorID, Telefono)
VALUES (7, 'Sergio', 'Pérez', 'DNI007', NULL, 5, '789-012-3456');

INSERT INTO Empleado (EmpleadoID, Nombre, Apellidos, DNI, EquipoID, SuperiorID, Telefono)
VALUES (8, 'George', 'Russell', 'DNI008', NULL, 4, '890-123-4567');

INSERT INTO Empleado (EmpleadoID, Nombre, Apellidos, DNI, EquipoID, SuperiorID, Telefono)
VALUES (9, 'Carlos', 'Sainz', 'DNI009', NULL, 6, '901-234-5678');

INSERT INTO Empleado (EmpleadoID, Nombre, Apellidos, DNI, EquipoID, SuperiorID, Telefono)
VALUES (10, 'Andreas', 'Seidl', 'DNI010', NULL, NULL, '012-345-6789');
INSERT INTO Empleado (EmpleadoID, Nombre, Apellidos, DNI, EquipoID, SuperiorID, Telefono)
VALUES (11, 'James', 'Kirk', 'DNI011', NULL, NULL, '012-345-6789');




INSERT INTO Equipo (EquipoID, NumIntegrantes, JefeEquipoID, FechaCreacion, NombreEquipo) VALUES (1, 20, 1, '20-11-1990', 'Mercedes-AMG Petronas');
INSERT INTO Equipo (EquipoID, NumIntegrantes, JefeEquipoID, FechaCreacion, NombreEquipo) VALUES (2, 15, 2, '02-10-2000', 'Red Bull Racing');
INSERT INTO Equipo (EquipoID, NumIntegrantes, JefeEquipoID, FechaCreacion, NombreEquipo) VALUES (3, 18, 3, '03-05-1990', 'Ferrari');
INSERT INTO Equipo (EquipoID, NumIntegrantes, JefeEquipoID, FechaCreacion, NombreEquipo) VALUES (4, 16, 4, '04-02-1990', 'Ducati Lenovo Team');
INSERT INTO Equipo (EquipoID, NumIntegrantes, JefeEquipoID, FechaCreacion, NombreEquipo) VALUES (5, 14, 5, '05-03-1990', 'Yamaha Factory Racing');
INSERT INTO Equipo (EquipoID, NumIntegrantes, JefeEquipoID, FechaCreacion, NombreEquipo) VALUES (6, 12, 6, '06-02-1990', 'Suzuki Ecstar');
INSERT INTO Equipo (EquipoID, NumIntegrantes, JefeEquipoID, FechaCreacion, NombreEquipo) VALUES (7, 15, 7, '07-10-1990', 'Aprilia Racing Team');
INSERT INTO Equipo (EquipoID, NumIntegrantes, JefeEquipoID, FechaCreacion, NombreEquipo) VALUES (8, 20, 8, '08-01-1990', 'Alpine F1 Team');
INSERT INTO Equipo (EquipoID, NumIntegrantes, JefeEquipoID, FechaCreacion, NombreEquipo) VALUES (9, 17, 9, '09-02-1990', 'HRC (Honda Racing Corporation)');
INSERT INTO Equipo (EquipoID, NumIntegrantes, JefeEquipoID, FechaCreacion, NombreEquipo) VALUES (10, 15,10, '10-05-1990', 'KTM Factory Racing');

INSERT INTO Patrocinador (PatrocinadorID, Nombre, ValorMonetario) VALUES (1, 'Red Bull', 5000000.00);
INSERT INTO Patrocinador (PatrocinadorID, Nombre, ValorMonetario) VALUES(2, 'Petronas', 4000000.00);
INSERT INTO Patrocinador (PatrocinadorID, Nombre, ValorMonetario) VALUES(3, 'Shell', 3000000.00);
INSERT INTO Patrocinador (PatrocinadorID, Nombre, ValorMonetario) VALUES(4, 'Pirelli', 2000000.00);
INSERT INTO Patrocinador (PatrocinadorID, Nombre, ValorMonetario) VALUES(5, 'Santander', 2500000.00);
INSERT INTO Patrocinador (PatrocinadorID, Nombre, ValorMonetario) VALUES(6, 'Monster Energy', 3500000.00);
INSERT INTO Patrocinador (PatrocinadorID, Nombre, ValorMonetario) VALUES(7, 'Marlboro', 4500000.00);
INSERT INTO Patrocinador (PatrocinadorID, Nombre, ValorMonetario) VALUES(8, 'Movistar', 1000000.00);
INSERT INTO Patrocinador (PatrocinadorID, Nombre, ValorMonetario) VALUES(9, 'Rolex', 1500000.00);
INSERT INTO Patrocinador (PatrocinadorID, Nombre, ValorMonetario) VALUES(10, 'Aramco', 6000000.00);





INSERT INTO Piloto (EmpleadoID, Superlicencia, EquipoID,  SustitutoID, IdIngeniero) VALUES (1, 'SL12345', 1,  NULL, 1);
INSERT INTO Piloto (EmpleadoID, Superlicencia, EquipoID,  SustitutoID, IdIngeniero) VALUES(2, 'SL23456', 2,  NULL, 2);
INSERT INTO Piloto (EmpleadoID, Superlicencia, EquipoID,  SustitutoID, IdIngeniero) VALUES(3, 'SL34567', 3,  NULL, 3);
INSERT INTO Piloto (EmpleadoID, Superlicencia, EquipoID,  SustitutoID, IdIngeniero) VALUES(4, 'SL45678', 4,  NULL, 4);
INSERT INTO Piloto (EmpleadoID, Superlicencia, EquipoID,  SustitutoID, IdIngeniero) VALUES(5, 'SL56789', 5,  NULL, 5);
INSERT INTO Piloto (EmpleadoID, Superlicencia, EquipoID,  SustitutoID, IdIngeniero) VALUES(6, 'SL67890', 6,  NULL, 6);
INSERT INTO Piloto (EmpleadoID, Superlicencia, EquipoID,  SustitutoID, IdIngeniero) VALUES(7, 'SL78901', 7,  NULL, 7);
INSERT INTO Piloto (EmpleadoID, Superlicencia, EquipoID,  SustitutoID, IdIngeniero) VALUES(8, 'SL89012', 8,  NULL, 8);
INSERT INTO Piloto (EmpleadoID, Superlicencia, EquipoID,  SustitutoID, IdIngeniero) VALUES(9, 'SL90123', 9,  NULL, 9);
INSERT INTO Piloto (EmpleadoID, Superlicencia, EquipoID,  SustitutoID, IdIngeniero) VALUES(10, 'SL01234', 10, NULL, 10);


INSERT INTO Mecanico (EmpleadoID, PosicionBoxes, EquipoID) VALUES (1, 'Frontal', 1);
INSERT INTO Mecanico (EmpleadoID, PosicionBoxes, EquipoID) VALUES(2, 'Lateral Izquierda', 2);
INSERT INTO Mecanico (EmpleadoID, PosicionBoxes, EquipoID) VALUES(3, 'Lateral Derecha', 3);
INSERT INTO Mecanico (EmpleadoID, PosicionBoxes, EquipoID) VALUES(4, 'Trasero', 4);
INSERT INTO Mecanico (EmpleadoID, PosicionBoxes, EquipoID) VALUES(5, 'Frontal', 5);
INSERT INTO Mecanico (EmpleadoID, PosicionBoxes, EquipoID) VALUES(6, 'Lateral Izquierda', 6);
INSERT INTO Mecanico (EmpleadoID, PosicionBoxes, EquipoID) VALUES(7, 'Lateral Derecha', 7);
INSERT INTO Mecanico (EmpleadoID, PosicionBoxes, EquipoID) VALUES(8, 'Trasero', 8);
INSERT INTO Mecanico (EmpleadoID, PosicionBoxes, EquipoID) VALUES(9, 'Frontal', 9);
INSERT INTO Mecanico (EmpleadoID, PosicionBoxes, EquipoID) VALUES(10, 'Lateral Izquierda', 10);

INSERT INTO IngenieroCarrera (EmpleadoID, PilotoID, EquipoID, DirigidoPor, Especialidad) VALUES (1, 1, 1, NULL, 'Aerodinámica');
INSERT INTO IngenieroCarrera (EmpleadoID, PilotoID, EquipoID, DirigidoPor, Especialidad) VALUES(2, 2, 2, NULL, 'Motor');
INSERT INTO IngenieroCarrera (EmpleadoID, PilotoID, EquipoID, DirigidoPor, Especialidad) VALUES(3, 3, 3, NULL, 'Chasis');
INSERT INTO IngenieroCarrera (EmpleadoID, PilotoID, EquipoID, DirigidoPor, Especialidad) VALUES(4, 4, 4, NULL, 'Suspensión');
INSERT INTO IngenieroCarrera (EmpleadoID, PilotoID, EquipoID, DirigidoPor, Especialidad) VALUES(5, 5, 5, NULL, 'Combustible');
INSERT INTO IngenieroCarrera (EmpleadoID, PilotoID, EquipoID, DirigidoPor, Especialidad) VALUES(6, 6, 6, NULL, 'Neumáticos');
INSERT INTO IngenieroCarrera (EmpleadoID, PilotoID, EquipoID, DirigidoPor, Especialidad) VALUES(7, 7, 7, NULL, 'Electrónica');
INSERT INTO IngenieroCarrera (EmpleadoID, PilotoID, EquipoID, DirigidoPor, Especialidad) VALUES(8, 8, 8, NULL, 'Transmisión');
INSERT INTO IngenieroCarrera (EmpleadoID, PilotoID, EquipoID, DirigidoPor, Especialidad) VALUES(9, 9, 9, NULL, 'Sistemas híbridos');
INSERT INTO IngenieroCarrera (EmpleadoID, PilotoID, EquipoID, DirigidoPor, Especialidad) VALUES(10, 10, 10, NULL, 'Diseño aerodinámico');

INSERT INTO Vehiculo (VehiculoID, Dimensiones, AñoFabricacion, VelMax, NumeroBastidor, Color, TipoRueda ) VALUES (1, '4.5x2.0x1.2', 2020, 320, 'BAS123456', 'Rojo', 'Pirelli' );
INSERT INTO Vehiculo (VehiculoID, Dimensiones, AñoFabricacion, VelMax, NumeroBastidor, Color, TipoRueda ) VALUES(2, '4.5x2.1x1.3', 2019, 310, 'BAS234567', 'Negro', 'Michelin' );
INSERT INTO Vehiculo (VehiculoID, Dimensiones, AñoFabricacion, VelMax, NumeroBastidor, Color, TipoRueda ) VALUES(3, '4.4x2.0x1.2', 2021, 315, 'BAS345678', 'Azul', 'Pirelli' );
INSERT INTO Vehiculo (VehiculoID, Dimensiones, AñoFabricacion, VelMax, NumeroBastidor, Color, TipoRueda ) VALUES(4, '4.6x2.1x1.4', 2018, 330, 'BAS456789', 'Verde', 'Bridgestone' );
INSERT INTO Vehiculo (VehiculoID, Dimensiones, AñoFabricacion, VelMax, NumeroBastidor, Color, TipoRueda ) VALUES(5, '4.7x2.2x1.3', 2020, 325, 'BAS567890', 'Amarillo', 'Michelin' );
INSERT INTO Vehiculo (VehiculoID, Dimensiones, AñoFabricacion, VelMax, NumeroBastidor, Color, TipoRueda ) VALUES(6, '4.5x2.0x1.1', 2021, 305, 'BAS678901', 'Blanco', 'Pirelli' );
INSERT INTO Vehiculo (VehiculoID, Dimensiones, AñoFabricacion, VelMax, NumeroBastidor, Color, TipoRueda ) VALUES(7, '4.6x2.2x1.3', 2019, 335, 'BAS789012', 'Gris', 'Bridgestone' );
INSERT INTO Vehiculo (VehiculoID, Dimensiones, AñoFabricacion, VelMax, NumeroBastidor, Color, TipoRueda ) VALUES(8, '4.4x2.1x1.4', 2020, 310, 'BAS890123', 'Negro', 'Pirelli' );
INSERT INTO Vehiculo (VehiculoID, Dimensiones, AñoFabricacion, VelMax, NumeroBastidor, Color, TipoRueda ) VALUES(9, '4.5x2.3x1.2', 2021, 320, 'BAS901234', 'Rojo', 'Michelin' );
INSERT INTO Vehiculo (VehiculoID, Dimensiones, AñoFabricacion, VelMax, NumeroBastidor, Color, TipoRueda ) VALUES(10, '4.7x2.0x1.1', 2018, 300, 'BAS012345', 'Verde', 'Pirelli' );

INSERT INTO Coche (VehiculoID, CocheID, ConfigMotor, Aerodinamica, Transmision) VALUES (1, 1, 'V6 Híbrido', 'Baja Resistencia', 'Automática');
INSERT INTO Coche (VehiculoID, CocheID, ConfigMotor, Aerodinamica, Transmision) VALUES(2, 2, 'V8', 'Media Resistencia', 'Manual');
INSERT INTO Coche (VehiculoID, CocheID, ConfigMotor, Aerodinamica, Transmision) VALUES(3, 3, 'V6', 'Alta Resistencia', 'Automática');
INSERT INTO Coche (VehiculoID, CocheID, ConfigMotor, Aerodinamica, Transmision) VALUES(4, 4, 'V12', 'Baja Resistencia', 'Manual');
INSERT INTO Coche (VehiculoID, CocheID, ConfigMotor, Aerodinamica, Transmision) VALUES(5, 5, 'V10', 'Alta Resistencia', 'Automática');
INSERT INTO Coche (VehiculoID, CocheID, ConfigMotor, Aerodinamica, Transmision) VALUES(6, 6, 'V6 Turbo', 'Media Resistencia', 'Manual');
INSERT INTO Coche (VehiculoID, CocheID, ConfigMotor, Aerodinamica, Transmision) VALUES(7, 7, 'V6 Híbrido', 'Baja Resistencia', 'Automática');
INSERT INTO Coche (VehiculoID, CocheID, ConfigMotor, Aerodinamica, Transmision) VALUES(8, 8, 'V8 Turbo', 'Media Resistencia', 'Manual');
INSERT INTO Coche (VehiculoID, CocheID, ConfigMotor, Aerodinamica, Transmision) VALUES(9, 9, 'V10', 'Alta Resistencia', 'Automática');
INSERT INTO Coche (VehiculoID, CocheID, ConfigMotor, Aerodinamica, Transmision) VALUES(10, 10, 'V12', 'Baja Resistencia', 'Manual');

INSERT INTO Moto (VehiculoID, MotoID,  AlturaAsiento, TipoManillar, CilindradaCC) VALUES (1, 11,  80.5, 'Estándar', 600);
INSERT INTO Moto (VehiculoID, MotoID,  AlturaAsiento, TipoManillar, CilindradaCC) VALUES(2, 12,  78.0, 'Deportivo', 1000);
INSERT INTO Moto (VehiculoID, MotoID,  AlturaAsiento, TipoManillar, CilindradaCC) VALUES(3, 13,  81.2, 'Café Racer', 750);
INSERT INTO Moto (VehiculoID, MotoID,  AlturaAsiento, TipoManillar, CilindradaCC) VALUES(4, 14,  79.3, 'Enduro', 850);
INSERT INTO Moto (VehiculoID, MotoID,  AlturaAsiento, TipoManillar, CilindradaCC) VALUES(5, 15,  77.8, 'Custom', 1200);
INSERT INTO Moto (VehiculoID, MotoID,  AlturaAsiento, TipoManillar, CilindradaCC) VALUES(6, 16,  80.0, 'Cruiser', 650);
INSERT INTO Moto (VehiculoID, MotoID,  AlturaAsiento, TipoManillar, CilindradaCC) VALUES(7, 17,  82.0, 'Deportivo', 1000);
INSERT INTO Moto (VehiculoID, MotoID,  AlturaAsiento, TipoManillar, CilindradaCC) VALUES(8, 18,  79.5, 'Naked', 900);
INSERT INTO Moto (VehiculoID, MotoID,  AlturaAsiento, TipoManillar, CilindradaCC) VALUES(9, 19,  81.0, 'Touring', 800);
INSERT INTO Moto (VehiculoID, MotoID,  AlturaAsiento, TipoManillar, CilindradaCC) VALUES(10, 20,  80.3, 'Adventure', 1100);




INSERT INTO Circuito (CircuitoID, Nombre, NumeroCurvas, SentidoGiro, Pais, Ciudad) VALUES (1, 'Monza', 11, 'Horario', 'Italia', 'Monza');
INSERT INTO Circuito (CircuitoID, Nombre, NumeroCurvas, SentidoGiro, Pais, Ciudad) VALUES(2, 'Silverstone', 18, 'Antihorario', 'Reino Unido', 'Silverstone');
INSERT INTO Circuito (CircuitoID, Nombre, NumeroCurvas, SentidoGiro, Pais, Ciudad) VALUES(3, 'Suzuka', 16, 'Horario', 'Japón', 'Suzuka');
INSERT INTO Circuito (CircuitoID, Nombre, NumeroCurvas, SentidoGiro, Pais, Ciudad) VALUES(4, 'Interlagos', 15, 'Antihorario', 'Brasil', 'Sao Paulo');
INSERT INTO Circuito (CircuitoID, Nombre, NumeroCurvas, SentidoGiro, Pais, Ciudad) VALUES(5, 'Catalunya', 14, 'Horario', 'España', 'Barcelona');
INSERT INTO Circuito (CircuitoID, Nombre, NumeroCurvas, SentidoGiro, Pais, Ciudad) VALUES(6, 'Yas Marina', 21, 'Antihorario', 'Emiratos Árabes Unidos', 'Abu Dhabi');
INSERT INTO Circuito (CircuitoID, Nombre, NumeroCurvas, SentidoGiro, Pais, Ciudad) VALUES(7, 'Spa-Francorchamps', 19, 'Horario', 'Bélgica', 'Stavelot');
INSERT INTO Circuito (CircuitoID, Nombre, NumeroCurvas, SentidoGiro, Pais, Ciudad) VALUES(8, 'Austin', 20, 'Antihorario', 'EEUU', 'Austin');
INSERT INTO Circuito (CircuitoID, Nombre, NumeroCurvas, SentidoGiro, Pais, Ciudad) VALUES(9, 'Imola', 13, 'Horario', 'Italia', 'Imola');
INSERT INTO Circuito (CircuitoID, Nombre, NumeroCurvas, SentidoGiro, Pais, Ciudad) VALUES(10, 'Zandvoort', 14, 'Antihorario', 'Países Bajos', 'Zandvoort');

INSERT INTO Calendario (Temporada, Fecha, CircuitoID, VehiculoID, PilotoID, EquipoID) VALUES (2024, '03-10-1990', 1, 1, 1, 1);
INSERT INTO Calendario (Temporada, Fecha, CircuitoID, VehiculoID, PilotoID, EquipoID) VALUES(2024, '04-05-1990', 2, 2, 2, 2);
INSERT INTO Calendario (Temporada, Fecha, CircuitoID, VehiculoID, PilotoID, EquipoID) VALUES(2024, '05-12-1990', 3, 3, 3, 3);
INSERT INTO Calendario (Temporada, Fecha, CircuitoID, VehiculoID, PilotoID, EquipoID) VALUES(2024, '06-08-1990', 4, 4, 4, 4);
INSERT INTO Calendario (Temporada, Fecha, CircuitoID, VehiculoID, PilotoID, EquipoID) VALUES(2024, '07-05-1990', 5, 5, 5, 5);
INSERT INTO Calendario (Temporada, Fecha, CircuitoID, VehiculoID, PilotoID, EquipoID) VALUES(2024, '08-03-1990', 6, 6, 6, 6);
INSERT INTO Calendario (Temporada, Fecha, CircuitoID, VehiculoID, PilotoID, EquipoID) VALUES(2024, '09-12-1990', 7, 7, 7, 7);
INSERT INTO Calendario (Temporada, Fecha, CircuitoID, VehiculoID, PilotoID, EquipoID) VALUES(2024, '10-02-1990', 8, 8, 8, 8);
INSERT INTO Calendario (Temporada, Fecha, CircuitoID, VehiculoID, PilotoID, EquipoID) VALUES(2024, '11-05-1990', 9, 9, 9, 9);
INSERT INTO Calendario (Temporada, Fecha, CircuitoID, VehiculoID, PilotoID, EquipoID) VALUES(2024, '12-04-1990', 10, 10, 10, 10);







INSERT INTO Entrenamiento (EntrenamientoID, EquipoID, Rendimiento, MejoraTiempo) VALUES (1, 1, 98.5, 1.234);
INSERT INTO Entrenamiento (EntrenamientoID, EquipoID, Rendimiento, MejoraTiempo) VALUES(2, 2, 97.3, 1.456);
INSERT INTO Entrenamiento (EntrenamientoID, EquipoID, Rendimiento, MejoraTiempo) VALUES(3, 3, 96.7, 1.789);
INSERT INTO Entrenamiento (EntrenamientoID, EquipoID, Rendimiento, MejoraTiempo) VALUES(4, 4, 95.4, 2.012);
INSERT INTO Entrenamiento (EntrenamientoID, EquipoID, Rendimiento, MejoraTiempo) VALUES(5, 5, 94.8, 1.678);
INSERT INTO Entrenamiento (EntrenamientoID, EquipoID, Rendimiento, MejoraTiempo) VALUES(6, 6, 93.6, 2.345);
INSERT INTO Entrenamiento (EntrenamientoID, EquipoID, Rendimiento, MejoraTiempo) VALUES(7, 7, 92.9, 2.456);
INSERT INTO Entrenamiento (EntrenamientoID, EquipoID, Rendimiento, MejoraTiempo) VALUES(8, 8, 91.8, 2.789);
INSERT INTO Entrenamiento (EntrenamientoID, EquipoID, Rendimiento, MejoraTiempo) VALUES(9, 9, 90.7, 1.890);
INSERT INTO Entrenamiento (EntrenamientoID, EquipoID, Rendimiento, MejoraTiempo) VALUES(10, 10, 89.5, 1.123);

INSERT INTO Carrera (CarreraID,VehiculoID, PilotoID, CircuitoID, NumeroEntradasBoxes, Accidente, NumVueltas, Tiempo,Puntos) VALUES (1,1, 1, 1, 2, 1, 53, '01:32:45',0);
INSERT INTO Carrera (CarreraID,VehiculoID, PilotoID, CircuitoID, NumeroEntradasBoxes, Accidente, NumVueltas, Tiempo,Puntos) VALUES (2, 1,2, 2, 1, 2, 52, '01:33:15',12);
INSERT INTO Carrera (CarreraID,VehiculoID, PilotoID, CircuitoID, NumeroEntradasBoxes, Accidente, NumVueltas, Tiempo,Puntos) VALUES (3, 1,3, 3, 3, 0, 56, '01:31:50',43);
INSERT INTO Carrera (CarreraID,VehiculoID, PilotoID, CircuitoID, NumeroEntradasBoxes, Accidente, NumVueltas, Tiempo,Puntos) VALUES (4, 1,4, 4, 2, 5, 55, '01:34:20',56);
INSERT INTO Carrera (CarreraID,VehiculoID, PilotoID, CircuitoID, NumeroEntradasBoxes, Accidente, NumVueltas, Tiempo,Puntos) VALUES (5, 1,5, 5, 1, 0, 57, '01:30:25',12);
INSERT INTO Carrera (CarreraID,VehiculoID, PilotoID, CircuitoID, NumeroEntradasBoxes, Accidente, NumVueltas, Tiempo,Puntos) VALUES (6, 1,6, 6, 2, 0, 58, '01:32:00',43);
INSERT INTO Carrera (CarreraID,VehiculoID, PilotoID, CircuitoID, NumeroEntradasBoxes, Accidente, NumVueltas, Tiempo,Puntos) VALUES (7, 1,7, 7, 3, 0, 54, '01:33:40',11);
INSERT INTO Carrera (CarreraID,VehiculoID, PilotoID, CircuitoID, NumeroEntradasBoxes, Accidente, NumVueltas, Tiempo,Puntos) VALUES (8, 1,8, 8, 1, 5, 59, '01:31:10',6);
INSERT INTO Carrera (CarreraID,VehiculoID, PilotoID, CircuitoID, NumeroEntradasBoxes, Accidente, NumVueltas, Tiempo,Puntos) VALUES (9, 1,9, 9, 2, 2, 60, '01:34:50',100);
INSERT INTO Carrera (CarreraID,VehiculoID, PilotoID, CircuitoID, NumeroEntradasBoxes, Accidente, NumVueltas, Tiempo,Puntos) VALUES (10,1, 10, 10, 3, 24, 61, '01:30:05',2);

INSERT INTO Proveedor (ProveedorID, Nombre) VALUES (1, 'Proveedor A');
INSERT INTO Proveedor (ProveedorID, Nombre) VALUES (2, 'Proveedor B');
INSERT INTO Proveedor (ProveedorID, Nombre) VALUES (3, 'Proveedor C');
INSERT INTO Proveedor (ProveedorID, Nombre) VALUES (4, 'Proveedor D');
INSERT INTO Proveedor (ProveedorID, Nombre) VALUES (5, 'Proveedor E');
INSERT INTO Proveedor (ProveedorID, Nombre) VALUES (6, 'Proveedor F');
INSERT INTO Proveedor (ProveedorID, Nombre) VALUES (7, 'Proveedor G');
INSERT INTO Proveedor (ProveedorID, Nombre) VALUES (8, 'Proveedor H');
INSERT INTO Proveedor (ProveedorID, Nombre) VALUES (9, 'Proveedor I');
INSERT INTO Proveedor (ProveedorID, Nombre) VALUES (10, 'Proveedor J');

INSERT INTO Contable (EmpleadoID, NumDespacho)
VALUES (1, 101);

INSERT INTO Contable (EmpleadoID, NumDespacho)
VALUES (2, 102);

INSERT INTO Contable (EmpleadoID, NumDespacho)
VALUES (3, 103);

INSERT INTO Contable (EmpleadoID, NumDespacho)
VALUES (4, 104);

INSERT INTO Contable (EmpleadoID, NumDespacho)
VALUES (5, 105);

INSERT INTO Contable (EmpleadoID, NumDespacho)
VALUES (6, 106);

INSERT INTO Contable (EmpleadoID, NumDespacho)
VALUES (7, 107);

INSERT INTO Contable (EmpleadoID, NumDespacho)
VALUES (8, 108);

INSERT INTO Contable (EmpleadoID, NumDespacho)
VALUES (9, 109);

INSERT INTO Contable (EmpleadoID, NumDespacho)
VALUES (10, 110);



INSERT INTO Factura (FacturaID, NumPiezas, Fechas, ContableID) VALUES (1, 5, '09-01-2013', 1);
INSERT INTO Factura (FacturaID, NumPiezas, Fechas, ContableID) VALUES(2, 10, '09-12-2013', 2);
INSERT INTO Factura (FacturaID, NumPiezas, Fechas, ContableID) VALUES(3, 8, '10-01-2013', 3);
INSERT INTO Factura (FacturaID, NumPiezas, Fechas, ContableID) VALUES(4, 6, '10-02-2013', 4);
INSERT INTO Factura (FacturaID, NumPiezas, Fechas, ContableID) VALUES(5, 12, '11-01-2013', 5);
INSERT INTO Factura (FacturaID, NumPiezas, Fechas, ContableID) VALUES(6, 4, '11-10-2013', 6);
INSERT INTO Factura (FacturaID, NumPiezas, Fechas, ContableID) VALUES(7, 9, '11-06-2013', 7);
INSERT INTO Factura (FacturaID, NumPiezas, Fechas, ContableID) VALUES(8, 7, '12-01-2013', 8);
INSERT INTO Factura (FacturaID, NumPiezas, Fechas, ContableID) VALUES(9, 3, '12-07-2013', 9);
INSERT INTO Factura (FacturaID, NumPiezas, Fechas, ContableID) VALUES(10, 11, '12-09-2013', 10);




INSERT INTO OperadorProduccion (EmpleadoID)
VALUES (1);

INSERT INTO OperadorProduccion (EmpleadoID)
VALUES (2);

INSERT INTO OperadorProduccion (EmpleadoID)
VALUES (3);

INSERT INTO OperadorProduccion (EmpleadoID)
VALUES (4);

INSERT INTO OperadorProduccion (EmpleadoID)
VALUES (7);

INSERT INTO OperadorProduccion (EmpleadoID)
VALUES (8);

INSERT INTO OperadorProduccion (EmpleadoID)
VALUES (9);

INSERT INTO OperadorProduccion (EmpleadoID)
VALUES (10);

INSERT INTO OperadorProduccion (EmpleadoID)
VALUES (5);

INSERT INTO OperadorProduccion (EmpleadoID)
VALUES (6);




INSERT INTO Pieza (PiezaID, NumeroSerie, Precio, Stock, Dimensiones, FechaVenta, Tipo, ProveedorID, VehiculoID, FacturaID, OperadorID) VALUES (1, 'PS12345', 1200.00, 15, '30x15x10', 2023, 'Motor', 1, 1, 1, 1);
INSERT INTO Pieza (PiezaID, NumeroSerie, Precio, Stock, Dimensiones, FechaVenta, Tipo, ProveedorID, VehiculoID, FacturaID, OperadorID) VALUES (2, 'PS23456', 850.00, 20, '25x10x8', 2023, 'Rueda', 2, 2, 2, 2);
INSERT INTO Pieza (PiezaID, NumeroSerie, Precio, Stock, Dimensiones, FechaVenta, Tipo, ProveedorID, VehiculoID, FacturaID, OperadorID) VALUES (3, 'PS34567', 1500.00, 10, '50x30x20', 2023, 'Chasis', 3, 3, 3, 3);
INSERT INTO Pieza (PiezaID, NumeroSerie, Precio, Stock, Dimensiones, FechaVenta, Tipo, ProveedorID, VehiculoID, FacturaID, OperadorID) VALUES (4, 'PS45678', 300.00, 30, '10x10x5', 2023, 'Neumático', 4, 4, 4, 4);
INSERT INTO Pieza (PiezaID, NumeroSerie, Precio, Stock, Dimensiones, FechaVenta, Tipo, ProveedorID, VehiculoID, FacturaID, OperadorID) VALUES (5, 'PS56789', 2000.00, 5, '60x40x30', 2023, 'Suspensión', 5, 5, 5, 5);
INSERT INTO Pieza (PiezaID, NumeroSerie, Precio, Stock, Dimensiones, FechaVenta, Tipo, ProveedorID, VehiculoID, FacturaID, OperadorID) VALUES (6, 'PS67890', 1000.00, 25, '20x15x10', 2023, 'Frenos', 6, 6, 6, 6);
INSERT INTO Pieza (PiezaID, NumeroSerie, Precio, Stock, Dimensiones, FechaVenta, Tipo, ProveedorID, VehiculoID, FacturaID, OperadorID) VALUES (7, 'PS78901', 700.00, 40, '15x10x8', 2023, 'Alerón', 7, 7, 7, 7);
INSERT INTO Pieza (PiezaID, NumeroSerie, Precio, Stock, Dimensiones, FechaVenta, Tipo, ProveedorID, VehiculoID, FacturaID, OperadorID) VALUES (8, 'PS89012', 900.00, 12, '35x20x15', 2023, 'Caja de Cambios', 8, 8, 8, 8);
INSERT INTO Pieza (PiezaID, NumeroSerie, Precio, Stock, Dimensiones, FechaVenta, Tipo, ProveedorID, VehiculoID, FacturaID, OperadorID) VALUES (9, 'PS90123', 1800.00, 8, '45x25x20', 2023, 'Motor', 9, 9, 9, 9);
INSERT INTO Pieza (PiezaID, NumeroSerie, Precio, Stock, Dimensiones, FechaVenta, Tipo, ProveedorID, VehiculoID, FacturaID, OperadorID) VALUES (10, 'PS01234', 400.00, 50, '12x12x10', 2023, 'Neumático', 10, 10, 10, 10);






INSERT INTO Contrato (ContratoID, EmpleadoID, FechaInicio, FechaFin, Descripcion, Salario) VALUES (1, 1, '01-01-2023', '01-01-2025', 'Contrato por 2 años con opción a renovación', 1500000);
INSERT INTO Contrato (ContratoID, EmpleadoID, FechaInicio, FechaFin, Descripcion, Salario) VALUES(2, 2, '01-02-2023', '01-02-2026', 'Contrato por 3 años', 2000000);
INSERT INTO Contrato (ContratoID, EmpleadoID, FechaInicio, FechaFin, Descripcion, Salario) VALUES(3, 3, '01-03-2023', '01-03-2024', 'Contrato por 1 año', 1800000);
INSERT INTO Contrato (ContratoID, EmpleadoID, FechaInicio, FechaFin, Descripcion, Salario) VALUES(4, 4, '01-04-2023', '01-04-2025', 'Contrato por 2 años', 2200000);
INSERT INTO Contrato (ContratoID, EmpleadoID, FechaInicio, FechaFin, Descripcion, Salario) VALUES(5, 5, '01-05-2023', '01-05-2026', 'Contrato por 3 años', 2500000);
INSERT INTO Contrato (ContratoID, EmpleadoID, FechaInicio, FechaFin, Descripcion, Salario) VALUES(6, 6, '01-06-2023', '01-06-2024', 'Contrato por 1 año con opción a extensión', 1700000);
INSERT INTO Contrato (ContratoID, EmpleadoID, FechaInicio, FechaFin, Descripcion, Salario) VALUES(7, 7, '01-07-2023', '01-07-2025', 'Contrato por 2 años', 2300000);
INSERT INTO Contrato (ContratoID, EmpleadoID, FechaInicio, FechaFin, Descripcion, Salario) VALUES(8, 8, '01-08-2023', '01-08-2026', 'Contrato por 3 años', 2100000);
INSERT INTO Contrato (ContratoID, EmpleadoID, FechaInicio, FechaFin, Descripcion, Salario) VALUES(9, 9, '01-09-2023', '01-09-2024', 'Contrato por 1 año', 1600000);
INSERT INTO Contrato (ContratoID, EmpleadoID, FechaInicio, FechaFin, Descripcion, Salario) VALUES(10, 10, '01-10-2023', '01-10-2025', 'Contrato por 2 años', 1900000);



INSERT INTO F1 (F1ID, Descripcion)
VALUES (1, 'Equipo dominante en la era híbrida con 7 títulos de pilotos');

INSERT INTO F1 (F1ID, Descripcion)
VALUES (2, 'Campeones del mundo con un enfoque agresivo en la ingeniería');

INSERT INTO F1 (F1ID, Descripcion)
VALUES (3, 'Equipo icónico, conocido por su legado en la F1 desde 1950');

INSERT INTO F1 (F1ID, Descripcion)
VALUES (4, 'Equipo histórico británico con varios campeonatos en su haber');

INSERT INTO F1 (F1ID, Descripcion)
VALUES (5, 'Equipo joven que ha crecido rápidamente en la parrilla');

INSERT INTO F1 (F1ID, Descripcion)
VALUES (6, 'Conocido por su enfoque técnico y su énfasis en el desarrollo');

INSERT INTO F1 (F1ID, Descripcion)
VALUES (7, 'Equipo estadounidense que compite con un presupuesto ajustado');

INSERT INTO F1 (F1ID, Descripcion)
VALUES (8, 'Equipo francés con una sólida herencia en la competición');

INSERT INTO F1 (F1ID, Descripcion)
VALUES (9, 'Equipo italiano con un enfoque en innovación y aerodinámica');

INSERT INTO F1 (F1ID, Descripcion)
VALUES (10, 'Equipo británico conocido por su pasión por el automovilismo');


INSERT INTO F2 (F2ID, Descripcion)
VALUES (1, 'Equipo que ha demostrado ser un contendiente fuerte en la F2');

INSERT INTO F2 (F2ID, Descripcion)
VALUES (2, 'Conocido por desarrollar jóvenes talentos para la F1');

INSERT INTO F2 (F2ID, Descripcion)
VALUES (3, 'Equipo con historia rica en la categoría de soporte de F1');

INSERT INTO F2 (F2ID, Descripcion)
VALUES (4, 'Históricamente, un equipo con gran éxito en la F2');

INSERT INTO F2 (F2ID, Descripcion)
VALUES (5, 'Famoso por sus innovaciones técnicas y diseño de coches');

INSERT INTO F2 (F2ID, Descripcion)
VALUES (6, 'Equipo que prioriza el rendimiento y la estrategia');

INSERT INTO F2 (F2ID, Descripcion)
VALUES (7, 'Con un enfoque en el desarrollo sostenible en el automovilismo');

INSERT INTO F2 (F2ID, Descripcion)
VALUES (8, 'Equipo que ha formado a varios campeones de F1');

INSERT INTO F2 (F2ID, Descripcion)
VALUES (9, 'Conocido por su feroz competitividad en la parrilla');

INSERT INTO F2 (F2ID, Descripcion)
VALUES (10, 'Equipo que promueve un fuerte espíritu de equipo y colaboración');

INSERT INTO MotoGP (MotoGPID, Descripcion)
VALUES (1, 'Equipo líder en el campeonato con múltiples títulos');

INSERT INTO MotoGP (MotoGPID, Descripcion)
VALUES (2, 'Famoso por su innovación y tecnología avanzada en motos');

INSERT INTO MotoGP (MotoGPID, Descripcion)
VALUES (3, 'Conocido por su fuerte rivalidad con otros equipos');

INSERT INTO MotoGP (MotoGPID, Descripcion)
VALUES (4, 'Equipo histórico con una rica tradición en motociclismo');

INSERT INTO MotoGP (MotoGPID, Descripcion)
VALUES (5, 'Destacado en el desarrollo de pilotos jóvenes y talentosos');

INSERT INTO MotoGP (MotoGPID, Descripcion)
VALUES (6, 'Reconocido por su estrategia efectiva en carrera');

INSERT INTO MotoGP (MotoGPID, Descripcion)
VALUES (7, 'Compite con un fuerte enfoque en la sostenibilidad');

INSERT INTO MotoGP (MotoGPID, Descripcion)
VALUES (8, 'Equipo que ha producido campeones legendarios');

INSERT INTO MotoGP (MotoGPID, Descripcion)
VALUES (9, 'Conocido por sus diseños innovadores y rendimiento superior');

INSERT INTO MotoGP (MotoGPID, Descripcion)
VALUES (10, 'Equipo que representa a su país con gran orgullo');





INSERT INTO JefeEquipo (EmpleadoID)
VALUES (11);  -- Lewis Hamilton, asumiendo que es un jefe de equipo





INSERT INTO EntrenamientoCarrera (VehiculoID, CircuitoID, PilotoID, EntrenamientoID, EquipoID, fecha)
VALUES (1, 1, 1, 1, 1, '15-03-2024');  -- Lewis Hamilton en Mercedes en Circuito 1




INSERT INTO EntrenamientoCarrera (VehiculoID, CircuitoID, PilotoID, EntrenamientoID, EquipoID, fecha)
VALUES (2, 3, 4, 1, 1, '18-03-2024');  -- Toto Wolff supervisando entrenamiento en Circuito 3


INSERT INTO EntrenamientoCarrera (VehiculoID, CircuitoID, PilotoID, EntrenamientoID, EquipoID, fecha)
VALUES (4, 1, 8, 1, 1, '22-03-2024');  -- George Russell en Circuito 1




INSERT INTO PilotoConduceVehiculo (PilotoID, VehiculoID)
VALUES (1, 1);  -- Lewis Hamilton conduce el Vehículo 1

INSERT INTO PilotoConduceVehiculo (PilotoID, VehiculoID)
VALUES (2, 2);  -- Max Verstappen conduce el Vehículo 2

INSERT INTO PilotoConduceVehiculo (PilotoID, VehiculoID)
VALUES (3, 3);  -- Charles Leclerc conduce el Vehículo 3

INSERT INTO PilotoConduceVehiculo (PilotoID, VehiculoID)
VALUES (4, 1);  -- Toto Wolff supervisa el Vehículo 1 (puede ser piloto en pruebas)

INSERT INTO PilotoConduceVehiculo (PilotoID, VehiculoID)
VALUES (5, 2);  -- Christian Horner supervisa el Vehículo 2 (puede ser piloto en pruebas)

INSERT INTO PilotoConduceVehiculo (PilotoID, VehiculoID)
VALUES (6, 3);  -- Mattia Binotto supervisa el Vehículo 3 (puede ser piloto en pruebas)

INSERT INTO PilotoConduceVehiculo (PilotoID, VehiculoID)
VALUES (7, 4);  -- Sergio Pérez conduce el Vehículo 4

INSERT INTO PilotoConduceVehiculo (PilotoID, VehiculoID)
VALUES (8, 5);  -- George Russell conduce el Vehículo 5

INSERT INTO PilotoConduceVehiculo (PilotoID, VehiculoID)
VALUES (9, 6);  -- Carlos Sainz conduce el Vehículo 6

INSERT INTO PilotoConduceVehiculo (PilotoID, VehiculoID)
VALUES (10, 7); -- Andreas Seidl, en contexto, puede supervisar o conducir un Vehículo 7







INSERT INTO PilotoCompiteCircuito (PilotoID, CircuitoID)
VALUES (1, 1);  -- Lewis Hamilton compite en el Circuito 1

INSERT INTO PilotoCompiteCircuito (PilotoID, CircuitoID)
VALUES (1, 2);  -- Lewis Hamilton compite en el Circuito 2

INSERT INTO PilotoCompiteCircuito (PilotoID, CircuitoID)
VALUES (2, 1);  -- Max Verstappen compite en el Circuito 1

INSERT INTO PilotoCompiteCircuito (PilotoID, CircuitoID)
VALUES (2, 3);  -- Max Verstappen compite en el Circuito 3

INSERT INTO PilotoCompiteCircuito (PilotoID, CircuitoID)
VALUES (3, 2);  -- Charles Leclerc compite en el Circuito 2

INSERT INTO PilotoCompiteCircuito (PilotoID, CircuitoID)
VALUES (3, 3);  -- Charles Leclerc compite en el Circuito 3

INSERT INTO PilotoCompiteCircuito (PilotoID, CircuitoID)
VALUES (4, 1);  -- Toto Wolff (suponiendo que compite en pruebas) en el Circuito 1

INSERT INTO PilotoCompiteCircuito (PilotoID, CircuitoID)
VALUES (5, 2);  -- Christian Horner en el Circuito 2 (en contextos de supervisión)

INSERT INTO PilotoCompiteCircuito (PilotoID, CircuitoID)
VALUES (6, 3);  -- Mattia Binotto compite en el Circuito 3 (como piloto en pruebas)

INSERT INTO PilotoCompiteCircuito (PilotoID, CircuitoID)
VALUES (7, 1);  -- Sergio Pérez compite en el Circuito 1






INSERT INTO PilotoTieneMecanico (PilotoID, MecanicoID)
VALUES (1, 1);  -- Lewis Hamilton tiene como mecánico al Mecánico 1

INSERT INTO PilotoTieneMecanico (PilotoID, MecanicoID)
VALUES (2, 2);  -- Max Verstappen tiene como mecánico al Mecánico 2

INSERT INTO PilotoTieneMecanico (PilotoID, MecanicoID)
VALUES (3, 3);  -- Charles Leclerc tiene como mecánico al Mecánico 3

INSERT INTO PilotoTieneMecanico (PilotoID, MecanicoID)
VALUES (4, 1);  -- Toto Wolff (en contexto, mecánico para pruebas) tiene como mecánico al Mecánico 1

INSERT INTO PilotoTieneMecanico (PilotoID, MecanicoID)
VALUES (5, 2);  -- Christian Horner tiene como mecánico al Mecánico 2

INSERT INTO PilotoTieneMecanico (PilotoID, MecanicoID)
VALUES (6, 3);  -- Mattia Binotto tiene como mecánico al Mecánico 3

INSERT INTO PilotoTieneMecanico (PilotoID, MecanicoID)
VALUES (7, 4);  -- Sergio Pérez tiene como mecánico al Mecánico 4

INSERT INTO PilotoTieneMecanico (PilotoID, MecanicoID)
VALUES (8, 5);  -- George Russell tiene como mecánico al Mecánico 5

INSERT INTO PilotoTieneMecanico (PilotoID, MecanicoID)
VALUES (9, 6);  -- Carlos Sainz tiene como mecánico al Mecánico 6

INSERT INTO PilotoTieneMecanico (PilotoID, MecanicoID)
VALUES (10, 7); -- Andreas Seidl tiene como mecánico al Mecánico 7





INSERT INTO VehiculoParticipaCircuito (VehiculoID, CircuitoID)
VALUES (1, 1);  -- Vehículo 1 participa en el Circuito 1

INSERT INTO VehiculoParticipaCircuito (VehiculoID, CircuitoID)
VALUES (1, 2);  -- Vehículo 1 participa en el Circuito 2

INSERT INTO VehiculoParticipaCircuito (VehiculoID, CircuitoID)
VALUES (2, 1);  -- Vehículo 2 participa en el Circuito 1

INSERT INTO VehiculoParticipaCircuito (VehiculoID, CircuitoID)
VALUES (2, 3);  -- Vehículo 2 participa en el Circuito 3

INSERT INTO VehiculoParticipaCircuito (VehiculoID, CircuitoID)
VALUES (3, 2);  -- Vehículo 3 participa en el Circuito 2

INSERT INTO VehiculoParticipaCircuito (VehiculoID, CircuitoID)
VALUES (3, 3);  -- Vehículo 3 participa en el Circuito 3

INSERT INTO VehiculoParticipaCircuito (VehiculoID, CircuitoID)
VALUES (4, 1);  -- Vehículo 4 participa en el Circuito 1

INSERT INTO VehiculoParticipaCircuito (VehiculoID, CircuitoID)
VALUES (5, 2);  -- Vehículo 5 participa en el Circuito 2

INSERT INTO VehiculoParticipaCircuito (VehiculoID, CircuitoID)
VALUES (5, 3);  -- Vehículo 5 participa en el Circuito 3

INSERT INTO VehiculoParticipaCircuito (VehiculoID, CircuitoID)
VALUES (6, 1);  -- Vehículo 6 participa en el Circuito 1



INSERT INTO CocheParticipaF1 (CocheID, F1ID)
VALUES (1, 1);  -- Coche 1 participa en la competición F1 1

INSERT INTO CocheParticipaF1 (CocheID, F1ID)
VALUES (1, 2);  -- Coche 1 participa en la competición F1 2

INSERT INTO CocheParticipaF1 (CocheID, F1ID)
VALUES (2, 1);  -- Coche 2 participa en la competición F1 1

INSERT INTO CocheParticipaF1 (CocheID, F1ID)
VALUES (2, 3);  -- Coche 2 participa en la competición F1 3

INSERT INTO CocheParticipaF1 (CocheID, F1ID)
VALUES (3, 2);  -- Coche 3 participa en la competición F1 2

INSERT INTO CocheParticipaF1 (CocheID, F1ID)
VALUES (3, 3);  -- Coche 3 participa en la competición F1 3

INSERT INTO CocheParticipaF1 (CocheID, F1ID)
VALUES (4, 1);  -- Coche 4 participa en la competición F1 1

INSERT INTO CocheParticipaF1 (CocheID, F1ID)
VALUES (5, 2);  -- Coche 5 participa en la competición F1 2

INSERT INTO CocheParticipaF1 (CocheID, F1ID)
VALUES (5, 3);  -- Coche 5 participa en la competición F1 3

INSERT INTO CocheParticipaF1 (CocheID, F1ID)
VALUES (6, 1);  -- Coche 6 participa en la competición F1 1

INSERT INTO CocheParticipaF2 (CocheID, F2ID)
VALUES (1, 1);  -- Coche 1 participa en la competición F2 1

INSERT INTO CocheParticipaF2 (CocheID, F2ID)
VALUES (1, 2);  -- Coche 1 participa en la competición F2 2

INSERT INTO CocheParticipaF2 (CocheID, F2ID)
VALUES (2, 1);  -- Coche 2 participa en la competición F2 1

INSERT INTO CocheParticipaF2 (CocheID, F2ID)
VALUES (2, 3);  -- Coche 2 participa en la competición F2 3

INSERT INTO CocheParticipaF2 (CocheID, F2ID)
VALUES (3, 2);  -- Coche 3 participa en la competición F2 2

INSERT INTO CocheParticipaF2 (CocheID, F2ID)
VALUES (3, 3);  -- Coche 3 participa en la competición F2 3

INSERT INTO CocheParticipaF2 (CocheID, F2ID)
VALUES (4, 1);  -- Coche 4 participa en la competición F2 1

INSERT INTO CocheParticipaF2 (CocheID, F2ID)
VALUES (5, 2);  -- Coche 5 participa en la compet

INSERT INTO MotoParticipaMotoGP (MotoID, MotoGPID)
VALUES (1, 1);  -- Moto 1 participa en la competición MotoGP 1

INSERT INTO MotoParticipaMotoGP (MotoID, MotoGPID)
VALUES (1, 2);  -- Moto 1 participa en la competición MotoGP 2

INSERT INTO MotoParticipaMotoGP (MotoID, MotoGPID)
VALUES (2, 1);  -- Moto 2 participa en la competición MotoGP 1

INSERT INTO MotoParticipaMotoGP (MotoID, MotoGPID)
VALUES (2, 3);  -- Moto 2 participa en la competición MotoGP 3

INSERT INTO MotoParticipaMotoGP (MotoID, MotoGPID)
VALUES (3, 2);  -- Moto 3 participa en la competición MotoGP 2

INSERT INTO MotoParticipaMotoGP (MotoID, MotoGPID)
VALUES (3, 3);  -- Moto 3 participa en la competición MotoGP 3

INSERT INTO MotoParticipaMotoGP (MotoID, MotoGPID)
VALUES (4, 1);  -- Moto 4 participa en la competición MotoGP 1

INSERT INTO MotoParticipaMotoGP (MotoID, MotoGPID)
VALUES (5, 2);  -- Moto 5 participa en la competición MotoGP 2

INSERT INTO MotoParticipaMotoGP (MotoID, MotoGPID)
VALUES (5, 3);  -- Moto 5 participa en la competición MotoGP 3

INSERT INTO MotoParticipaMotoGP (MotoID, MotoGPID)
VALUES (6, 1);  -- Moto 6 participa en la competición MotoGP 1





INSERT INTO PatrocinadorPatrocinaEquipo (PatrocinadorID, EquipoID, Temporada) VALUES (1, 1, '2024');
INSERT INTO PatrocinadorPatrocinaEquipo (PatrocinadorID, EquipoID, Temporada) VALUES(2, 2, '2024');
INSERT INTO PatrocinadorPatrocinaEquipo (PatrocinadorID, EquipoID, Temporada) VALUES(3, 3, '2024');
INSERT INTO PatrocinadorPatrocinaEquipo (PatrocinadorID, EquipoID, Temporada) VALUES(4, 4, '2024');
INSERT INTO PatrocinadorPatrocinaEquipo (PatrocinadorID, EquipoID, Temporada) VALUES(5, 5, '2024');
INSERT INTO PatrocinadorPatrocinaEquipo (PatrocinadorID, EquipoID, Temporada) VALUES(6, 6, '2024');
INSERT INTO PatrocinadorPatrocinaEquipo (PatrocinadorID, EquipoID, Temporada) VALUES(7, 7, '2024');
INSERT INTO PatrocinadorPatrocinaEquipo (PatrocinadorID, EquipoID, Temporada) VALUES(8, 8, '2024');
INSERT INTO PatrocinadorPatrocinaEquipo (PatrocinadorID, EquipoID, Temporada) VALUES(9, 9, '2024');
INSERT INTO PatrocinadorPatrocinaEquipo (PatrocinadorID, EquipoID, Temporada) VALUES(10, 10, '2024');



SELECT * FROM   Empleado;
SELECT * FROM   Equipo;
SELECT * FROM  Patrocinador ;
SELECT * FROM   Piloto;
SELECT * FROM  Mecanico ;
SELECT * FROM   IngenieroCarrera;
SELECT * FROM   Vehiculo;
SELECT * FROM  Coche ;
SELECT * FROM  Moto ;
SELECT * FROM  Circuito ;
SELECT * FROM  Calendario ;
SELECT * FROM  Entrenamiento ;
SELECT * FROM   Carrera;
SELECT * FROM   Proveedor;
SELECT * FROM   Pieza;
SELECT * FROM  Contable ;
SELECT * FROM  Factura ;
SELECT * FROM  Contrato ;
SELECT * FROM  OperadorProduccion ;
SELECT * FROM  F1 ;
SELECT * FROM  F2 ;
SELECT * FROM   MotoGP;
SELECT * FROM  JefeEquipo ;
SELECT * FROM   EntrenamientoCarrera;
SELECT * FROM  PilotoConduceVehiculo ;
SELECT * FROM  PilotoCompiteCircuito ;
SELECT * FROM  PilotoTieneMecanico ;
SELECT * FROM   VehiculoParticipaCircuito;
SELECT * FROM   CocheParticipaF1;
SELECT * FROM   CocheParticipaF2;
SELECT * FROM  MotoParticipaMotoGP ;
SELECT * FROM  PatrocinadorPatrocinaEquipo ;

SELECT * FROM  Vista_Puntos ;
SELECT * FROM  Patrocinios_Temporada ;


 


CREATE OR REPLACE
PROCEDURE clasificacion (anhoActual IN NUMBER)
IS
    
    regCarreras Carrera%ROWTYPE;

    
    Nombre VARCHAR2(100);
    idPiloto NUMBER;
    idPilotoAnterior NUMBER := 0;
    puntos NUMBER := 0;

   
    CURSOR C_Carreras IS
        SELECT *
        FROM Carrera Car
        WHERE CarreraID IN (
            SELECT CarreraID
            FROM Calendario
            WHERE Temporada = anhoActual
        )
        ORDER BY Car.PilotoID;

BEGIN
    
    DBMS_OUTPUT.PUT_LINE('Clasificación de la Temporada ' || anhoActual);
    DBMS_OUTPUT.PUT_LINE('');

   
    OPEN C_Carreras;

   
    LOOP
        FETCH C_Carreras INTO regCarreras;
        EXIT WHEN C_Carreras%NOTFOUND;

        IF regCarreras.PilotoID = idPilotoAnterior OR idPilotoAnterior = 0 THEN
           
            puntos := puntos + regCarreras.Puntos;
            idPilotoAnterior := regCarreras.PilotoID;
        ELSE
           
            SELECT Nombre INTO Nombre
            FROM Empleado
            WHERE EmpleadoID = idPilotoAnterior;

            DBMS_OUTPUT.PUT_LINE('El piloto ' || Nombre || ' tiene ' || puntos || ' puntos.');

          
            puntos := regCarreras.Puntos;
            idPilotoAnterior := regCarreras.PilotoID;
        END IF;
    END LOOP;

   
    IF idPilotoAnterior != 0 THEN
        SELECT Nombre INTO Nombre
        FROM Empleado
        WHERE EmpleadoID = idPilotoAnterior;

        DBMS_OUTPUT.PUT_LINE('El piloto ' || Nombre || ' tiene ' || puntos || ' puntos.');
    END IF;

   
    CLOSE C_Carreras;


EXCEPTION
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE('No se encontraron datos para la temporada especificada.');
    WHEN VALUE_ERROR THEN
        DBMS_OUTPUT.PUT_LINE('Error en el manejo de valores. Verifique los datos ingresados.');
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('Ocurrió un error inesperado: ' || SQLERRM);

    
    IF C_Carreras%ISOPEN THEN
        CLOSE C_Carreras;
    END IF;
END clasificacion;
/
CREATE OR REPLACE
FUNCTION valorProveedor(idProveedor IN NUMBER)
RETURN DECIMAL
IS
    CURSOR C_Piezas IS
        SELECT Precio
        FROM Pieza
        WHERE PROVEEDORID = idProveedor;

    regPieza C_Piezas%ROWTYPE;
    suma DECIMAL := 0;

   
    ex_cursor_error EXCEPTION;
BEGIN
   
    OPEN C_Piezas;

   
    LOOP
        FETCH C_Piezas INTO regPieza;
        EXIT WHEN C_Piezas%NOTFOUND;

        suma := suma + regPieza.Precio;
    END LOOP;

   
    CLOSE C_Piezas;

   
    RETURN suma;


EXCEPTION
   
    WHEN ex_cursor_error THEN
        CLOSE C_Piezas;
        RAISE_APPLICATION_ERROR(-20001, 'Error al manejar el cursor.');

   
    WHEN VALUE_ERROR THEN
        CLOSE C_Piezas;
        RAISE_APPLICATION_ERROR(-20002, 'Error en el cálculo, posible valor NULL.');

  
    WHEN NO_DATA_FOUND THEN
        RETURN 0;

   
    WHEN OTHERS THEN
        CLOSE C_Piezas;
        RAISE_APPLICATION_ERROR(-20003, 'Error inesperado: ' || SQLERRM);
END valorProveedor;
/
CREATE OR REPLACE 
PROCEDURE mostrarVehiculo(vehiculoIDext IN NUMBER)
IS
    sumaPrecio DECIMAL := 0;
    regPiezas Pieza%ROWTYPE;

   
    CURSOR C_Piezas IS
        SELECT * 
        FROM Pieza  
        WHERE VehiculoID = vehiculoIDext;

BEGIN 
  
    DBMS_OUTPUT.PUT_LINE('Piezas del Vehículo ' || vehiculoIDext);
    DBMS_OUTPUT.PUT_LINE('');
    
   
    OPEN C_Piezas;

    
    LOOP
        FETCH C_Piezas INTO regPiezas;
        EXIT WHEN C_Piezas%NOTFOUND;

    
        DBMS_OUTPUT.PUT_LINE('Pieza con Nº Serie: ' || regPiezas.NumeroSerie || 
                             ' del tipo ' || regPiezas.Tipo || 
                             '. Precio: ' || regPiezas.Precio);

       
        sumaPrecio := sumaPrecio + regPiezas.Precio;
    END LOOP;

    
    CLOSE C_Piezas;

    
    DBMS_OUTPUT.PUT_LINE('');
    DBMS_OUTPUT.PUT_LINE('El precio total de las piezas del coche es: ' || sumaPrecio);


EXCEPTION
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE('No se encontraron piezas para el vehículo con ID: ' || vehiculoIDext);

    WHEN VALUE_ERROR THEN
        DBMS_OUTPUT.PUT_LINE('Error en los datos. Verifique los valores asociados a las piezas o al vehículo.');

    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('Ocurrió un error inesperado: ' || SQLERRM);

  
    IF C_Piezas%ISOPEN THEN
        CLOSE C_Piezas;
    END IF;
END mostrarVehiculo;
/

create or replace 
function presupuestoTotal
RETURN DECIMAL
is
    sumatotal DECIMAL:=0;
    regPiezas Pieza%ROWTYPE;
    CURSOR C_Piezas is
        select * from Pieza;
    regContrato Contrato%ROWTYPE;
    CURSOR C_Contrato is
        select * from Contrato;



begin 


    OPEN C_Piezas;

    LOOP
        FETCH C_Piezas into regPiezas;
        exit when C_Piezas%NOTFOUND;

            sumatotal:=sumatotal + regPiezas.Precio;
            
    end loop;


    open C_Contrato;
    LOOP
        FETCH C_Contrato into regContrato;
        exit when C_Contrato%NOTFOUND;

            sumatotal:=sumatotal + regContrato.Salario;
            
    end loop;

    return sumatotal;

end presupuestoTotal;

/


create or replace 
function presupuestoEquipo(ID in Number)
RETURN number
is
    sumatotal DECIMAL:=0;
    regPiezas Pieza%ROWTYPE;
    CURSOR C_Piezas is
        select * from Pieza where vehiculoID in (select vehiculoID from Coche where vehiculoID = ID)
        OR vehiculoID in (select vehiculoID from Moto where vehiculoID = ID);
    regContrato Contrato%ROWTYPE;
    CURSOR C_Contrato is
        select * from Contrato where EmpleadoID in (select EmpleadoID from Empleado where EquipoID = ID);



begin 


    OPEN C_Piezas;

    LOOP
        FETCH C_Piezas into regPiezas;
        exit when C_Piezas%NOTFOUND;

            sumatotal:=sumatotal + regPiezas.Precio;
            
    end loop;

    open c_Contrato;
    LOOP
        FETCH C_Contrato into regContrato;
        exit when C_Contrato%NOTFOUND;

            sumatotal:=sumatotal + regContrato.Salario;
            
    end loop;

    return sumatotal;



end presupuestoEquipo;


/

CREATE OR REPLACE 
PROCEDURE ajusteIRPF(Indice IN NUMBER)
IS
    regContrato Contrato%ROWTYPE;
    CURSOR C_Contrato IS
        SELECT * 
        FROM Contrato
        FOR UPDATE; 

BEGIN 
   
    OPEN C_Contrato;

    LOOP
        FETCH C_Contrato INTO regContrato;
        EXIT WHEN C_Contrato%NOTFOUND;

        
        UPDATE Contrato 
        SET Salario = CAST((Salario * (100 + Indice)) / 100 AS NUMBER)
        WHERE CURRENT OF C_Contrato;
    END LOOP;

    
    CLOSE C_Contrato;

   
    DBMS_OUTPUT.PUT_LINE('Se ha actualizado el salario de todos los empleados con un índice del ' || Indice || '%');


EXCEPTION
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE('No se encontraron contratos para actualizar.');
    
    WHEN VALUE_ERROR THEN
        DBMS_OUTPUT.PUT_LINE('Error en los datos. Verifique el índice proporcionado.');

    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('Ocurrió un error inesperado: ' || SQLERRM);

 
    IF C_Contrato%ISOPEN THEN
        CLOSE C_Contrato;
    END IF;

END ajusteIRPF;
/

BEGIN
  
    DBMS_OUTPUT.PUT_LINE('El presupuesto total : ' || presupuestoTotal());
END;

/
BEGIN
clasificacion(2024);
END;
/
SELECT valorProveedor(1) AS ValorPiezasProve FROM DUAL;
/
BEGIN
mostrarVehiculo(2);
END;
/


BEGIN
  
    DBMS_OUTPUT.PUT_LINE('El presupuesto  del equipo es: ' || presupuestoEquipo(1));
END;
/

BEGIN
    ajusteIRPF(10); 
END;
/
SELECT Salario FROM Contrato;
