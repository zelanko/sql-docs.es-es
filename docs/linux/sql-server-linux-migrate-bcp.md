---
title: Copia masiva de datos a SQL Server en Linux | Documentos de Microsoft
description: 
author: sanagama
ms.author: sanagama
manager: jhubbard
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.assetid: 7b93d0d7-7946-4b78-b33a-57d6307cdfa9
ms.workload: On Demand
ms.openlocfilehash: 5796872eb1f2a0a7cdcdcd895081df6169669240
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="bulk-copy-data-with-bcp-to-sql-server-on-linux"></a>Datos de copia masiva con bcp para SQL Server en Linux

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

Este tema muestra cómo utilizar el [bcp](../tools/bcp-utility.md) utilidad de línea de comandos para la copia masiva de datos entre una instancia de SQL Server 2017 en Linux y un archivo de datos en un formato especificado por el usuario.

Puede usar `bcp` para importar grandes cantidades de filas en tablas de SQL Server o para exportar datos de tablas de SQL Server a archivos de datos. Excepto cuando se usa con la opción queryout, `bcp` no requiere ningún conocimiento de Transact-SQL. El `bcp` utilidad de línea de comandos funciona con Microsoft SQL Server que se ejecutan de forma local o en la nube, en Linux, Windows o Docker y base de datos de SQL Azure y almacenamiento de datos de SQL Azure.

En este tema le mostrará cómo para:
- Importar datos en una tabla mediante el `bcp in` comando
- Exportar datos de una tabla de usar el `bcp out` comando

## <a name="install-the-sql-server-command-line-tools"></a>Instalar las herramientas de línea de comandos de SQL Server

`bcp`forma parte de las herramientas de línea de comandos de SQL Server, que no se instalan automáticamente con SQL Server en Linux. Si no ha instalado ya las herramientas de línea de comandos de SQL Server en el equipo Linux, debe instalarlos. Para obtener más información sobre cómo instalar las herramientas, seleccione la distribución de Linux en la lista siguiente:

- [Red Hat Enterprise Linux (RHEL)](sql-server-linux-setup-tools.md#RHEL)
- [Ubuntu](sql-server-linux-setup-tools.md#ubuntu)
- [SUSE Linux Enterprise Server (SLES)](sql-server-linux-setup-tools.md#SLES)

## <a name="import-data-with-bcp"></a>Importar datos con bcp

En este tutorial, creará una base de datos de ejemplo y una tabla en la instancia local de SQL Server (**localhost**) y, a continuación, usar `bcp` para cargar en la tabla de ejemplo de un archivo de texto en el disco.

### <a name="create-a-sample-database-and-table"></a>Crear una base de datos de ejemplo y una tabla

Empecemos creando una base de datos de ejemplo con una tabla sencilla que se utilizarán en el resto de este tutorial.

1. En el cuadro de Linux, abra un terminal de comando.

2. Copie y pegue los comandos siguientes en la ventana de terminal. Estos comandos usan el **sqlcmd** utilidad de línea de comandos para crear una base de datos de ejemplo (**BcpSampleDB**) y una tabla (**TestEmployees**) en la instancia local de SQL Server (**localhost**). No olvide reemplazar la `username` y `<your_password>` según sea necesario antes de ejecutar los comandos.

Crear la base de datos **BcpSampleDB**:
```bash 
sqlcmd -S localhost -U sa -P <your_password> -Q "CREATE DATABASE BcpSampleDB;"
```
Crear la tabla **TestEmployees** en la base de datos **BcpSampleDB**:
```bash 
sqlcmd -S localhost -U sa -P <your_password> -d BcpSampleDB -Q "CREATE TABLE TestEmployees (Id INT IDENTITY(1,1) NOT NULL PRIMARY KEY, Name NVARCHAR(50), Location NVARCHAR(50));"
```
### <a name="create-the-source-data-file"></a>Crear el archivo de datos de origen
Copie y pegue el comando siguiente en la ventana de terminal. Se usará la integrada `cat` comando para crear un archivo de datos de texto de ejemplo con 3 registros guarde el archivo en su directorio particular como **~/test_data.txt**. Los campos de los registros están delimitados por punto y coma.

```bash
cat > ~/test_data.txt << EOF
1,Jared,Australia
2,Nikita,India
3,Tom,Germany
EOF
```

También puede comprobar que se creó correctamente el archivo de datos ejecutando el comando siguiente en la ventana de terminal:
```bash 
cat ~/test_data.txt
```

Debería mostrarse lo siguiente en la ventana de terminal:
```bash
1,Jared,Australia
2,Nikita,India
3,Tom,Germany
```

### <a name="import-data-from-the-source-data-file"></a>Importar datos desde el archivo de datos de origen
Copie y pegue los comandos siguientes en la ventana de terminal. Este comando usa `bcp` para conectarse a la instancia local de SQL Server (**localhost**) e importar los datos del archivo de datos (**~/test_data.txt**) en la tabla (**TestEmployees**) en la base de datos (**BcpSampleDB**). No olvide reemplazar el nombre de usuario y `<your_password>` según sea necesario antes de ejecutar los comandos.

```bash 
bcp TestEmployees in ~/test_data.txt -S localhost -U sa -P <your_password> -d BcpSampleDB -c -t  ','
```

Esta es una breve descripción de los parámetros de línea de comandos que se utiliza con `bcp` en este ejemplo:
- `-S`: especifica la instancia de SQL Server que se va a conectar
- `-U`: especifica el inicio de sesión identificador usado para conectarse a SQL Server
- `-P`: especifica la contraseña para el identificador de inicio de sesión
- `-d`: especifica la base de datos para conectarse a
- `-c`: realiza operaciones con un tipo de datos de caracteres
- `-t`: especifica el terminador de campo. Estamos utilizando `comma` como terminador de campo para los registros en nuestro archivo de datos

> [!NOTE]
> No se está especificando un terminador de fila personalizado en este ejemplo. Filas en el archivo de datos de texto se cancelaron correctamente con `newline` cuando se utiliza el `cat` comando para crear el archivo de datos de versiones anteriores.

Puede comprobar que se importaron correctamente los datos al ejecutar el comando siguiente en la ventana de terminal. No olvide reemplazar la `username` y `<your_password>` según sea necesario antes de ejecutar el comando.
```bash 
sqlcmd -S localhost -d BcpSampleDB -U sa -P <your_password> -I -Q "SELECT * FROM TestEmployees;"
```

Esto debería mostrar los siguientes resultados:
```bash
Id          Name                Location
----------- ------------------- -------------------
          1 Jared               Australia
          2 Nikita              India
          3 Tom                 Germany

(3 rows affected)
```

## <a name="export-data-with-bcp"></a>Exportar los datos con bcp

En este tutorial, va a usar `bcp` para exportar datos de la tabla de ejemplo que hemos creado con anterioridad a un nuevo archivo de datos.

Copie y pegue los comandos siguientes en la ventana de terminal. Estos comandos usan el `bcp` utilidad de línea de comandos para exportar datos de la tabla **TestEmployees** en la en la base de datos **BcpSampleDB** a un nuevo archivo de datos denominado **~/test_export.txt**.  No olvide reemplazar el nombre de usuario y `<your_password>` según sea necesario antes de ejecutar el comando.

```bash 
bcp TestEmployees out ~/test_export.txt -S localhost -U sa -P <your_password> -d BcpSampleDB -c -t ','
```

También puede comprobar que los datos se ha exportado correctamente al ejecutar el comando siguiente en la ventana de terminal:
```bash 
cat ~/test_export.txt
```

Debería mostrarse lo siguiente en la ventana de terminal:
```
1,Jared,Australia
2,Nikita,India
3,Tom,Germany
```

## <a name="see-also"></a>Vea también
- [bcp, utilidad](../tools/bcp-utility.md)
- [Formatos de datos por razones de compatibilidad mediante bcp](../relational-databases/import-export/specify-data-formats-for-compatibility-when-using-bcp-sql-server.md)
- [Importación masiva de datos mediante el uso de INSERCIÓN masiva](../relational-databases/import-export/import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)
- [BULK INSERT (Transact-SQL)](../t-sql/statements/bulk-insert-transact-sql.md)
