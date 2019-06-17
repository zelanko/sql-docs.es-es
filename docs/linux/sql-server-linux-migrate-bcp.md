---
title: Copia masiva de datos a SQL Server en Linux | Microsoft Docs
description: ''
author: rothja
ms.author: jroth
manager: craigg
ms.date: 01/30/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 7b93d0d7-7946-4b78-b33a-57d6307cdfa9
ms.openlocfilehash: bda200cccdaadb4db30b95289c2e16982a4e1f4b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66713138"
---
# <a name="bulk-copy-data-with-bcp-to-sql-server-on-linux"></a>Copia masiva de datos con bcp para SQL Server en Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

En este artículo se muestra cómo usar el [bcp](../tools/bcp-utility.md) utilidad de línea de comandos para la copia masiva de datos entre una instancia de SQL Server en Linux y un archivo de datos en un formato especificado por el usuario.

Puede usar `bcp` para importar grandes cantidades de filas en tablas de SQL Server o para exportar datos de tablas de SQL Server a archivos de datos. Excepto cuando se usa con la opción queryout, `bcp` exige ningún conocimiento de Transact-SQL. El `bcp` utilidad de línea de comandos funciona con Microsoft SQL Server que se ejecutan en local o en la nube, en Linux, Windows o Docker y Azure SQL Database y Azure SQL Data Warehouse.

En este artículo aprenderá a:
- Importar datos en una tabla mediante el `bcp in` comando
- Exportar datos de una tabla mediante el `bcp out` comando

## <a name="install-the-sql-server-command-line-tools"></a>Instalar las herramientas de línea de comandos de SQL Server

`bcp` forma parte de las herramientas de línea de comandos de SQL Server, que no se instalan automáticamente con SQL Server en Linux. Si no ha instalado ya las herramientas de línea de comandos de SQL Server en su equipo Linux, debe instalarlos. Para obtener más información sobre cómo instalar las herramientas, seleccione la distribución de Linux en la lista siguiente:

- [Red Hat Enterprise Linux (RHEL)](sql-server-linux-setup-tools.md#RHEL)
- [Ubuntu](sql-server-linux-setup-tools.md#ubuntu)
- [SUSE Linux Enterprise Server (SLES)](sql-server-linux-setup-tools.md#SLES)

## <a name="import-data-with-bcp"></a>Importar datos con bcp

En este tutorial, creará una base de datos de ejemplo y una tabla en la instancia de SQL Server local (**localhost**) y, a continuación, usar `bcp` para cargar en la tabla de ejemplo de un archivo de texto en el disco.

### <a name="create-a-sample-database-and-table"></a>Crear una base de datos de ejemplo y una tabla

Comencemos por crear una base de datos de ejemplo con una tabla sencilla que se usa en el resto de este tutorial.

1. En el cuadro de Linux, abra un terminal de comandos.

2. Copie y pegue los siguientes comandos en la ventana de terminal. Estos comandos usan el **sqlcmd** utilidad de línea de comandos para crear una base de datos de ejemplo (**BcpSampleDB**) y una tabla (**TestEmployees**) en la instancia local de SQL Server (**localhost**). No olvide reemplazar el `username` y `<your_password>` según sea necesario antes de ejecutar los comandos.

Crear la base de datos **BcpSampleDB**:
```bash 
sqlcmd -S localhost -U sa -P <your_password> -Q "CREATE DATABASE BcpSampleDB;"
```
Crear la tabla **TestEmployees** en la base de datos **BcpSampleDB**:
```bash 
sqlcmd -S localhost -U sa -P <your_password> -d BcpSampleDB -Q "CREATE TABLE TestEmployees (Id INT IDENTITY(1,1) NOT NULL PRIMARY KEY, Name NVARCHAR(50), Location NVARCHAR(50));"
```
### <a name="create-the-source-data-file"></a>Crear el archivo de datos de origen
Copie y pegue el siguiente comando en la ventana del terminal. Usamos los integrados `cat` comando para crear un archivo de datos de texto de ejemplo con tres registros guarde el archivo en su directorio particular como **~/test_data.txt**. Los campos en los registros están delimitados por punto y coma.

```bash
cat > ~/test_data.txt << EOF
1,Jared,Australia
2,Nikita,India
3,Tom,Germany
EOF
```

Puede comprobar que el archivo de datos se creó correctamente ejecutando el comando siguiente en la ventana del terminal:
```bash 
cat ~/test_data.txt
```

Esto debería mostrar lo siguiente en la ventana del terminal:
```bash
1,Jared,Australia
2,Nikita,India
3,Tom,Germany
```

### <a name="import-data-from-the-source-data-file"></a>Importar datos desde el archivo de datos de origen
Copie y pegue los siguientes comandos en la ventana de terminal. Este comando usa `bcp` para conectarse a la instancia de SQL Server local (**localhost**) e importar los datos del archivo de datos ( **~/test_data.txt**) en la tabla (**TestEmployees** ) en la base de datos (**BcpSampleDB**). No olvide reemplazar el nombre de usuario y `<your_password>` según sea necesario antes de ejecutar los comandos.

```bash 
bcp TestEmployees in ~/test_data.txt -S localhost -U sa -P <your_password> -d BcpSampleDB -c -t  ','
```

Aquí es una breve descripción de los parámetros de línea de comandos que se utiliza con `bcp` en este ejemplo:
- `-S`: especifica la instancia de SQL Server que se va a conectar
- `-U`: especifica el identificador se usa para conectarse a SQL Server de inicio de sesión
- `-P`: especifica la contraseña para el identificador de inicio de sesión
- `-d`: especifica la base de datos para conectarse a
- `-c`: lleva a cabo operaciones con un tipo de datos de caracteres
- `-t`: especifica el terminador de campo. Estamos usando `comma` como terminador de campo para los registros de nuestro archivo de datos

> [!NOTE]
> En este ejemplo, no vamos a especificar un terminador de fila personalizado. Se cancelaron correctamente las filas en el archivo de datos de texto con `newline` cuando se usa el `cat` comando para crear el archivo de datos anteriormente.

Puede comprobar que los datos se importen correctamente ejecutando el comando siguiente en la ventana del terminal. No olvide reemplazar el `username` y `<your_password>` según sea necesario antes de ejecutar el comando.
```bash 
sqlcmd -S localhost -d BcpSampleDB -U sa -P <your_password> -I -Q "SELECT * FROM TestEmployees;"
```

Esto debería mostrar los resultados siguientes:
```bash
Id          Name                Location
----------- ------------------- -------------------
          1 Jared               Australia
          2 Nikita              India
          3 Tom                 Germany

(3 rows affected)
```

## <a name="export-data-with-bcp"></a>Exportación de datos con bcp

En este tutorial, usará `bcp` para exportar datos de la tabla de ejemplo que hemos creado anteriormente a un nuevo archivo de datos.

Copie y pegue los siguientes comandos en la ventana de terminal. Estos comandos usan el `bcp` utilidad de línea de comandos para exportar datos de la tabla **TestEmployees** en la base de datos **BcpSampleDB** a un nuevo archivo de datos denominado **~/test_export.txt** .  No olvide reemplazar el nombre de usuario y `<your_password>` según sea necesario antes de ejecutar el comando.

```bash 
bcp TestEmployees out ~/test_export.txt -S localhost -U sa -P <your_password> -d BcpSampleDB -c -t ','
```

Puede comprobar que los datos se exportaron correctamente ejecutando el comando siguiente en la ventana del terminal:
```bash 
cat ~/test_export.txt
```

Esto debería mostrar lo siguiente en la ventana del terminal:
```
1,Jared,Australia
2,Nikita,India
3,Tom,Germany
```

## <a name="see-also"></a>Vea también
- [bcp, utilidad](../tools/bcp-utility.md)
- [Formatos de datos por razones de compatibilidad mediante bcp](../relational-databases/import-export/specify-data-formats-for-compatibility-when-using-bcp-sql-server.md)
- [Importación masiva de datos mediante el uso de BULK INSERT](../relational-databases/import-export/import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)
- [BULK INSERT (Transact-SQL)](../t-sql/statements/bulk-insert-transact-sql.md)
