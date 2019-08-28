---
title: Usar tipos de tipo Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f133fa066ef2c486cf7bb40c5b653c99e077bc46
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 08/14/2019
ms.locfileid: "69026941"
---
# <a name="using-spatial-datatypes"></a>Empleo de tipos de datos espaciales

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Se admiten los tipos de objeto espaciales (Geometry y Geography) al iniciar JDBC driver Preview 6.5.0. Actualmente, no se admiten los tipos de los tipos de los tipos de los parámetros de tabla (TVP), BulkCopy y Always Encrypted. En esta página se muestran varios casos de uso de tipos de datos Geometry y Geography con el controlador JDBC. Para obtener información general sobre los tipos de datos espaciales, consulte la página de [información general de tipos de datos espaciales](https://docs.microsoft.com/sql/relational-databases/spatial/spatial-data-types-overview) .

## <a name="creating-a-geometry--geography-object"></a>Creación de un objeto Geometry/Geography

Hay dos formas principales de crear un objeto Geometry/Geography, ya sea convertir de un texto conocido (WKT) o de un archivo binario conocido (WKB).

### <a name="creating-from-wkt"></a>Crear a partir de WKT

```java
String geoWKT = "LINESTRING(1 0, 0 1, -1 0)";
Geometry geomWKT = Geometry.STGeomFromText(geoWKT, 0);
Geography geogWKT = Geography.STGeomFromText(geoWKT, 4326);
```

Esto creará un objeto Geometry LINESTRING con el identificador del sistema de referencia espacial (SRID) 0 y un objeto Geography con SRID 4326.

### <a name="creating-from-wkb"></a>Crear a partir de WKB

```java
byte[] geomWKB = Hex.decodeHex("00000000010403000000000000000000F03F00000000000000000000000000000000000000000000F03F000000000000F0BF000000000000000001000000010000000001000000FFFFFFFF0000000002".toCharArray());
byte[] geogWKB = Hex.decodeHex("E61000000104030000000000000000000000000000000000F03F000000000000F03F00000000000000000000000000000000000000000000F0BF01000000010000000001000000FFFFFFFF0000000002".toCharArray());

Geometry geomWKT = Geometry.deserialize(geomWKB);
Geography geogWKT = Geography.deserialize(geogWKB);
```

Esto creará un objeto Geometry y Geography que es equivalente a los creados a partir del WKT previamente.

## <a name="working-with-a-geometry--geography-object"></a>Trabajar con un objeto Geometry/Geography

Suponiendo que el usuario tenga una tabla en SQL Server como se indica a continuación:

```sql
CREATE TABLE sampleTable (c1 geometry)  
```

Un script de ejemplo para insertar un valor de geometría sería:

```java
String geoWKT = "LINESTRING(1 0, 0 1, -1 0)";
Geometry geomWKT = Geometry.STGeomFromText(geoWKT, 0);
SQLServerPreparedStatement pstmt = (SQLServerPreparedStatement) connection.prepareStatement("insert into sampleTable values (?)");
pstmt.setGeometry(1, geomWKT);  
pstmt.execute();
```

Lo mismo se puede hacer para el homólogo de geografía, mediante una columna Geography y un método **setGeography ()** .

Para leer una columna Geometry/Geography:

```java
try(SQLServerResultSet rs = (SQLServerResultSet)stmt.executeQuery("select * from geomTable")) {
    while(rs.next()){
        rs.getGeometry(1);
    }
}
```

Lo mismo se puede hacer para el homólogo de geografía, mediante una columna Geography y un método **getGeography ()** .

## <a name="newly-introduced-apis"></a>API recién introducidas

Estas son las nuevas API públicas que se introdujeron con esta adición, en las clases **SQLServerPreparedStatement**, **SQLServerResultSet**, **Geometry**y **Geography**.

### <a name="sqlserverpreparedstatement"></a>SQLServerPreparedStatement

|Método|Descripción|
|:------|:----------|
|void setGeometry (int n, Geometry x)| Establece el parámetro designado en el objeto de clase Microsoft. SQL. Geometry especificado.
|void setGeography (int n, Geography x)| Establece el parámetro designado para el objeto de la clase Microsoft. SQL. Geography dado.

### <a name="sqlserverresultset"></a>SQLServerResultSet

|Método|Descripción|
|:------|:----------|
|Geometry getGeometry (int colunIndex)| Devuelve el valor de la columna designada en la fila actual de este objeto ResultSet como un objeto com. Microsoft. SqlServer. JDBC. Geometry en el lenguaje de programación Java.
|Geometry getGeometry (String columnName)| Devuelve el valor de la columna designada en la fila actual de este objeto ResultSet como un objeto com. Microsoft. SqlServer. JDBC. Geometry en el lenguaje de programación Java.
|Geography getGeography (int colunIndex)| Devuelve el valor de la columna designada en la fila actual de este objeto ResultSet como un objeto com. Microsoft. SqlServer. JDBC. Geography en el lenguaje de programación Java.
|Geography getGeography (String columnName)| Devuelve el valor de la columna designada en la fila actual de este objeto ResultSet como un objeto com. Microsoft. SqlServer. JDBC. Geography en el lenguaje de programación Java.

### <a name="geometry"></a>Geometry

|Método|Descripción|
|:------|:----------|
|Geometry STGeomFromText (String WKT, int SRID)| Constructor para una instancia de Geometry a partir de una representación Well-Known Text (WKT) de Open Geospatial Consortium (OGC), ampliada con los valores Z (elevación) y M (medida) pertenecientes a la instancia.
|Geometry STGeomFromWKB(byte[] wkb)| Constructor para una instancia de Geometry a partir de una representación Well-Known Binary (WKB) de Open Geospatial Consortium (OGC).
|Deserialización de geometrías (Byte [] WKB)| Constructor de una instancia de Geometry a partir de un formato interno de SQL Server para los datos espaciales.
|Geometry Parse (String WKT)| Constructor para una instancia de Geometry a partir de una representación Well-Known Text (WKT) de Open Geospatial Consortium (OGC). El identificador de referencia espacial se toma como valor predeterminado 0.
|Punto de geometría (Double x, Double y, int SRID)| Constructor de una instancia de Geometry que representa una instancia de Point a partir de sus valores X e y y un identificador de referencia espacial.
|String STAsText ()| Devuelve la representación Well-Known Text (WKT) de Open Geospatial Consortium (OGC) de una instancia de Geometry. Este texto no contendrá ningún valor Z (elevación) ni M (medida) perteneciente a la instancia.
|byte[] STAsBinary()| Devuelve la representación Well-Known Binary (WKB) de Open Geospatial Consortium (OGC) de una instancia de Geometry. Este valor no contendrá ningún valor Z o M perteneciente a la instancia.
|byte[] serialize()| Devuelve los bytes que representan un formato interno de SQL Server del tipo Geometry.
|Boolean hasM ()| Devuelve si el objeto contiene un valor M (medida).
|Boolean hasZ ()| Devuelve si el objeto contiene un valor Z (elevación).
|Double getX ()| Devuelve el valor de la coordenada X.
|Double getY ()| Devuelve el valor de la coordenada Y.
|Double getM ()| Devuelve el valor M (medida) del objeto.
|Double getZ ()| Devuelve el valor Z (elevación) del objeto.
|int getSrid()| Devuelve el valor del identificador de referencia espacial (SRID).
|valor booleano isNull ()| Devuelve si el objeto Geometry es NULL.
|int STNumPoints()| Devuelve el número de puntos del objeto Geometry.
|String STGeometryType()| Devuelve el nombre del tipo de Open Geospatial Consortium (OGC) representado por una instancia de Geometry.
|String asTextZM()| Devuelve la representación Well-Known Text (WKT) del objeto Geometry.
|String toString()| Devuelve la representación de la cadena del objeto Geometry.

### <a name="geography"></a>Geografía

|Método|Descripción|
|:------|:----------|
|Geography STGeomFromText (String WKT, int SRID)| Constructor para una instancia de Geography a partir de una representación Well-Known Text (WKT) de Open Geospatial Consortium (OGC), ampliada con los valores Z (elevación) y M (medida) pertenecientes a la instancia.
|Geography STGeomFromWKB(byte[] wkb)| Constructor para una instancia de Geography a partir de una representación Well-Known Binary (WKB) de Open Geospatial Consortium (OGC).
|Geography deserialize(byte[] wkb)| Constructor para una instancia de Geography a partir de un formato interno de SQL Server para los datos espaciales.
|Análisis de Geografía (String WKT)| Constructor para una instancia de Geography a partir de una representación Well-Known Text (WKT) de Open Geospatial Consortium (OGC). El identificador de referencia espacial se toma como valor predeterminado 0.
|Punto de Geografía (Double Lon, Double lat, int SRID)| Constructor para una instancia de Geography que representa una instancia de Point a partir de su longitud y latitud y un identificador de referencia espacial.
|String STAsText ()| Devuelve la representación Well-Known Text (WKT) de Open Geospatial Consortium (OGC) de una instancia de Geography. Este texto no contendrá ningún valor Z (elevación) ni M (medida) perteneciente a la instancia.
|byte[] STAsBinary())| Devuelve la representación Well-Known Binary (WKB) de Open Geospatial Consortium (OGC) de una instancia de Geography. Este valor no contendrá ningún valor Z o M perteneciente a la instancia.
|byte[] serialize()| Devuelve los bytes que representan un formato interno de SQL Server del tipo Geography.
|Boolean hasM ()| Devuelve si el objeto contiene un valor M (medida).
|Boolean hasZ ()| Devuelve si el objeto contiene un valor Z (elevación).
|Double getLatitude ()| Devuelve el valor de latitud.
|Double getLongitude()| Devuelve el valor de longitud.
|Double getM ()| Devuelve el valor M (medida) del objeto.
|Double getZ ()| Devuelve el valor Z (elevación) del objeto.
|int getSrid()| Devuelve el valor del identificador de referencia espacial (SRID).
|valor booleano isNull ()| Devuelve si el objeto Geography es NULL.
|int STNumPoints()| Devuelve el número de puntos en el objeto Geography.
|String STGeographyType()| Devuelve el nombre del tipo de Open Geospatial Consortium (OGC) representado por una instancia de Geography.
|String asTextZM()| Devuelve la representación Well-Known Text (WKT) del objeto Geography.
|String toString()| Devuelve la representación de la cadena del objeto Geography.

## <a name="limitations-of-spatial-datatypes"></a>Limitaciones de los tipos de los tipos de texto espaciales

1. Los subtipos de **CircularString**, **CompoundCurve**, **CurvePolygon**y **FullGlobe** espaciales solo se admiten a partir de SQL Server 2012 y versiones posteriores.

2. No se puede usar Always Encrypted con tipos de los tipos de los tipos de

3. Actualmente no se admiten las operaciones de procedimientos almacenados, TVP y BulkCopy en los tipos de los tipos de los tipos de

## <a name="see-also"></a>Vea también

[Ejemplo de tipos de datos espaciales (JDBC)](../../connect/jdbc/spatial-data-types-sample.md)
