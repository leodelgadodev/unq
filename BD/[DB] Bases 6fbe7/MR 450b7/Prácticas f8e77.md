# Prácticas

## Star Trek

IMPERIO<codigoGalactico_imperio (PK), nombre, temperatura>

FLOTA<codigoGalactico_flota (PK), destino, {mision}, codigoGalactico_imperio (FK)>

RAZA<nombre_raza (PK), {habilidad}>

PLANETA<nombre_planeta (PK), pob, coords, {(montaña_temp, montaña_nombre)}, codigoGalactico_imperio (FK)>

CAPITAN<codigoGalactico_capitan (PK), nombre, codigoGalactico_imperio (FK), nombre_planeta (FK)>

NAVE<codigo (PK), vMax, energiaAcum, codigoGalactico_flota (PK, FK), codigoGalactico_capitan (FK)>

MANIOBRA<nombre (PK), energiaReq>

SABE_REALIZAR<codigo_nave (PK, FK), nombre_maniobra (PK, FK)>

HABITADO_POR<porcentajePob, nombre_planeta (PK, FK), nombre_raza (PK, FK)>

## Asociación de Astronomía

RADAR<#serie (PK), modelo, posicion>

REEMPLAZA<#serie_reemplaza_a (FK), #serie_esReemplazado_por (PK, FK)>

GRUPO_DE_INVESTIGACION<pais (PK), nombreGrupo (PK), #serie (FK), {premio}, (fechaInicio_dia, fechaInicio_anho, fechaInicio_mes)>

SEDE<numero (PK), pais (FK), nombreGrupo (FK), ubicacion, cantInvestigadores>

INVESTIGADOR<legajo (PK), numero (PK, FK), especializacion, fechaNacimiento>

INSTITUTO<ciudad (PK), nombre (PK), director, {(lineaFinanciam_montoAnual, lineaFinanciam_nombre, lineaFinanciam_anho)}>

SISTEMA_SOLAR<cantPlanetas, promEdad, coord1 (PK), coord2 (PK), distancia (PK), pais (FK)>

PLANETA<nombre (PK), superficie, tempPromedio, coord1 (FK), coord2 (FK), distancia (FK)>

SATELITE<codigo (PK), superficie, edadPromedio, {crater}, nombre (PK, FK)>

FINANCIA<ciudad (PK, FK), nombre (PK, FK), legajo (PK, FK), numero (PK, FK)>

ESTUDIA<fechaInicio, hora, coord1 (PK, FK), coord2 (PK, FK), pais (PK, FK), nombreGrupo (PK, FK)>