---
description: Empleo de tipos de datos espaciales
title: Empleo de tipos de datos espaciales | Microsoft Docs
ms.custom: ''
ms.date: 07/31/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 02b545ec1d33d17674266d58a2a120f07af423ad
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/05/2020
ms.locfileid: "91727532"
---
# <a name="using-spatial-datatypes"></a>Empleo de tipos de datos espaciales

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Los tipos de datos espaciales (Geometry y Geography) se admiten a partir de la versión 6.5.0 en vista previa del controlador JDBC. Actualmente, no se admiten los tipos de datos espaciales con procedimientos almacenados, parámetros con valores de tabla (TVP), BulkCopy y Always Encrypted. En esta página se muestran diversos casos de uso de los tipos de datos Geometry y Geography con el controlador JDBC. Para obtener información general sobre los tipos de datos espaciales, compruebe la página [Información general de los tipos de datos espaciales](../../relational-databases/spatial/spatial-data-types-overview.md).

## <a name="creating-a-geometry--geography-object"></a>Creación de un objeto Geometry o Geography

Hay dos formas principales de crear un objeto Geometry o Geography: convertir desde un formato Well-Known Text (WKT) o desde un formato de SQL Server interno (WKB).

### <a name="creating-from-wkt"></a>Creación a partir de WKT

```java
String geoWKT = "LINESTRING(1 0, 0 1, -1 0)";
Geometry geomWKT = Geometry.STGeomFromText(geoWKT, 0);
Geography geogWKT = Geography.STGeomFromText(geoWKT, 4326);
```

Se creará un objeto Geometry LINESTRING con el valor del identificador del sistema de referencia (SRID) 0 y un objeto Geography con SRID 4326.

### <a name="creating-from-clr"></a>Creación a partir de CLR

```java
byte[] geomCLR = Hex.decodeHex("00000000010403000000000000000000F03F00000000000000000000000000000000000000000000F03F000000000000F0BF000000000000000001000000010000000001000000FFFFFFFF0000000002".toCharArray());
byte[] geogCLR = Hex.decodeHex("E61000000104030000000000000000000000000000000000F03F000000000000F03F00000000000000000000000000000000000000000000F0BF01000000010000000001000000FFFFFFFF0000000002".toCharArray());

Geometry geomWKT = Geometry.deserialize(geomCLR);
Geography geogWKT = Geography.deserialize(geogCLR);
```

Se creará un objeto Geometry y Geography equivalente a los creados a partir de WKT anteriormente.

## <a name="working-with-a-geometry--geography-object"></a>Uso de un objeto Geometry o Geography

Suponiendo que el usuario tenga una tabla en SQL Server como la que se muestra a continuación:

```sql
CREATE TABLE sampleTable (c1 geometry)  
```

Un script de ejemplo para insertar un valor Geometry sería:

```java
String geoWKT = "LINESTRING(1 0, 0 1, -1 0)";
Geometry geomWKT = Geometry.STGeomFromText(geoWKT, 0);
SQLServerPreparedStatement pstmt = (SQLServerPreparedStatement) connection.prepareStatement("insert into sampleTable values (?)");
pstmt.setGeometry(1, geomWKT);  
pstmt.execute();
```

Puede hacerse lo mismo para el homólogo de Geography, mediante una columna Geograophy y el método **setGeography()**.

Para leer una columna Geometry o Geography:

```java
try(SQLServerResultSet rs = (SQLServerResultSet)stmt.executeQuery("select * from geomTable")) {
    while(rs.next()){
        rs.getGeometry(1);
    }
}
```

Puede hacerse lo mismo para el homólogo de Geography, mediante una columna Geography y el método **getGeography()**.

## <a name="newly-introduced-apis"></a>API recién presentadas

Estas son las nuevas API públicas que se introdujeron con esta adición, en las clases **SQLServerPreparedStatement**, **SQLServerResultSet**, **Geometry**y **Geography**.

### <a name="sqlserverpreparedstatement"></a>SQLServerPreparedStatement

|Método|Descripción|
|:------|:----------|
|void setGeometry(int n, Geometry x)| Establece el parámetro designado en el objeto de clase microsoft.sql.Geometry especificado.
|void setGeography(int n, Geography x)| Establece el parámetro designado en el objeto de clase microsoft.sql.Geography especificado.

### <a name="sqlserverresultset"></a>SQLServerResultSet

|Método|Descripción|
|:------|:----------|
|Geometry getGeometry(int colunIndex)| Recupera el valor de la columna designada en la fila actual de este objeto ResultSet como un objeto com.microsoft.sqlserver.jdbc.Geometry en el lenguaje de programación Java.
|Geometry getGeometry(String columnName)| Recupera el valor de la columna designada en la fila actual de este objeto ResultSet como un objeto com.microsoft.sqlserver.jdbc.Geometry en el lenguaje de programación Java.
|Geography getGeography(int colunIndex)| Recupera el valor de la columna designada en la fila actual de este objeto ResultSet como un objeto com.microsoft.sqlserver.jdbc.Geography en el lenguaje de programación Java.
|Geography getGeography(String columnName)| Recupera el valor de la columna designada en la fila actual de este objeto ResultSet como un objeto com.microsoft.sqlserver.jdbc.Geography en el lenguaje de programación Java.

### <a name="geometry"></a>Geometría

|Método|Descripción|
|:------|:----------|
|Geometry STGeomFromText(String wkt, int SRID)| Constructor para una instancia de Geometry a partir de una representación Well-Known Text (WKT) de Open Geospatial Consortium (OGC), ampliada con los valores Z (elevación) y M (medida) pertenecientes a la instancia.
|Geometry STGeomFromWKB(byte[] wkb)| Constructor para una instancia de Geometry a partir de una representación Well-Known Binary (WKB) de Open Geospatial Consortium (OGC). Nota: Actualmente, este método usa el formato de SQL Server interno (CLR) para crear una instancia de Geometry. Este es un problema conocido en el controlador y está previsto cambiarlo para que acepte en su lugar los datos de WKB. En el caso de los usuarios existentes que ya usan este método, considere la posibilidad de cambiar a deserialize(byte).
|Geometries deserialize(byte[] clr)| Constructor para una instancia de Geometry a partir de un formato interno de SQL Server para datos espaciales.
|Geometry parse(String wkt)| Constructor para una instancia de Geometry a partir de una representación Well-Known Text (WKT) de Open Geospatial Consortium (OGC). El identificador de referencia espacial se establece en 0 de forma predeterminada.
|Geometry point(double x, double y, int SRID)| Constructor para una instancia de Geography que representa una instancia de Point a partir de sus valores de X e Y, y un identificador de referencia espacial.
|String STAsText()| Devuelve la representación Well-Known Text (WKT) de Open Geospatial Consortium (OGC) de una instancia de Geometry. Este texto no contendrá ningún valor Z (elevación) ni M (medida) perteneciente a la instancia.
|byte[] STAsBinary()| Devuelve la representación del formato de SQL Server interno (CLR) de una instancia de Geometry. Este valor no contendrá ningún valor Z o M perteneciente a la instancia.
|byte[] serialize()| Devuelve los bytes que representan un formato interno de SQL Server del tipo Geometry.
|boolean hasM()| Devuelve si el objeto contiene un valor M (medida).
|boolean hasZ()| Devuelve si el objeto contiene un valor Z (elevación).
|Double getX()| Devuelve el valor de la coordenada X.
|Double getY()| Devuelve el valor de la coordenada Y.
|Double getM()| Devuelve el valor M (medida) del objeto.
|Double getZ()| Devuelve el valor Z (elevación) del objeto.
|int getSrid()| Devuelve el valor del identificador de referencia espacial (SRID).
|boolean isNull()| Devuelve si el objeto Geometry es NULL.
|int STNumPoints()| Devuelve el número de puntos del objeto Geometry.
|String STGeometryType()| Devuelve el nombre del tipo de Open Geospatial Consortium (OGC) representado por una instancia de Geometry.
|String asTextZM()| Devuelve la representación Well-Known Text (WKT) del objeto Geometry.
|String toString()| Devuelve la representación de la cadena del objeto Geometry.

### <a name="geography"></a>Geography

|Método|Descripción|
|:------|:----------|
|Geography STGeomFromText(String wkt, int SRID)| Constructor para una instancia de Geography a partir de una representación Well-Known Text (WKT) de Open Geospatial Consortium (OGC), ampliada con los valores Z (elevación) y M (medida) pertenecientes a la instancia.
|Geography STGeomFromWKB(byte[] wkb)| Constructor para una instancia de Geography a partir de una representación Well-Known Binary (WKB) de Open Geospatial Consortium (OGC). Nota: Este método usa actualmente el formato de SQL Server interno (CLR) para crear una instancia de Geometry, pero en el futuro se cambiará para que acepte en su lugar los datos de WKB, puesto que el homólogo de SQL Server de este método (STGeomFromWKB) usa WKB. En el caso de los usuarios existentes que ya usan este método, considere la posibilidad de cambiar a deserialize(byte).
|Geography deserialize(byte[] clr)| Constructor para una instancia de Geography a partir de un formato interno de SQL Server para datos espaciales.
|Geography parse(String wkt)| Constructor para una instancia de Geography a partir de una representación Well-Known Text (WKT) de Open Geospatial Consortium (OGC). El identificador de referencia espacial se establece en 0 de forma predeterminada.
|Geography point(double lon, double lat, int SRID)| Constructor para una instancia de Geography que representa una instancia de Point a partir de su longitud y latitud y un identificador de referencia espacial.
|String STAsText()| Devuelve la representación Well-Known Text (WKT) de Open Geospatial Consortium (OGC) de una instancia de Geography. Este texto no contendrá ningún valor Z (elevación) ni M (medida) perteneciente a la instancia.
|byte[] STAsBinary())| Devuelve la representación del formato de SQL Server interno (CLR) de una instancia de Geography. Este valor no contendrá ningún valor Z o M perteneciente a la instancia.
|byte[] serialize()| Devuelve los bytes que representan un formato interno de SQL Server del tipo Geography.
|boolean hasM()| Devuelve si el objeto contiene un valor M (medida).
|boolean hasZ()| Devuelve si el objeto contiene un valor Z (elevación).
|Double getLatitude()| Devuelve el valor de latitud.
|Double getLongitude()| Devuelve el valor de longitud.
|Double getM()| Devuelve el valor M (medida) del objeto.
|Double getZ()| Devuelve el valor Z (elevación) del objeto.
|int getSrid()| Devuelve el valor del identificador de referencia espacial (SRID).
|boolean isNull()| Devuelve si el objeto Geography es NULL.
|int STNumPoints()| Devuelve el número de puntos del objeto Geography.
|String STGeographyType()| Devuelve el nombre del tipo de Open Geospatial Consortium (OGC) representado por una instancia de Geography.
|String asTextZM()| Devuelve la representación Well-Known Text (WKT) del objeto Geography.
|String toString()| Devuelve la representación de la cadena del objeto Geography.

## <a name="limitations-of-spatial-datatypes"></a>Limitaciones de los tipos de datos espaciales

1. Los subtipos espaciales **CircularString**, **CompoundCurve**, **CurvePolygon** y **FullGlobe** solo se admiten a partir de SQL Server 2012 y versiones posteriores.

2. No se puede usar Always Encrypted con los tipos de datos espaciales.

3. Actualmente no se admiten los procedimientos almacenados, TVP ni las operaciones BulkCopy con los tipos de datos espaciales.

## <a name="see-also"></a>Consulte también

[Ejemplo de tipos de datos espaciales (JDBC)](../../connect/jdbc/spatial-data-types-sample.md)