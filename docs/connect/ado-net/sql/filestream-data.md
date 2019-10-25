---
title: Datos de FILESTREAM
description: Describe cómo trabajar con datos de valores grandes almacenados en SQL Server 2008 con el atributo FILESTREAM.
ms.date: 08/15/2019
ms.assetid: bd8b845c-0f09-4295-b466-97ef106eefa8
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 83e793fac40a8e41850f2a45e138dd125130c13e
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452211"
---
# <a name="filestream-data"></a>Datos de FILESTREAM

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[Descargar ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

El atributo de almacenamiento FILESTREAM es para los datos binarios (BLOB) almacenados en una columna varbinary (Max). Antes de FILESTREAM, el almacenamiento de datos binarios requería un tratamiento especial. Los datos no estructurados, como los documentos de texto, las imágenes y el vídeo, se suelen almacenar fuera de la base de datos, por lo que resulta difícil de administrar.

> [!NOTE]
> Debe instalar el .NET Framework 3,5 SP1 (o posterior) o .NET Core para trabajar con datos de FILESTREAM mediante SqlClient.

La especificación del atributo FILESTREAM en una columna varbinary(max) provoca que SQL Server almacene los datos en el sistema de archivos NTFS local en lugar de hacerlo en el archivo de base de datos. Aunque se almacenan por separado, puede usar las mismas instrucciones de Transact-SQL admitidas para trabajar con los datos varbinary(max) almacenados en la base de datos.

## <a name="sqlclient-support-for-filestream"></a>Compatibilidad de SqlClient con FILESTREAM

El proveedor de datos SqlClient de Microsoft para SQL Server, <xref:Microsoft.Data.SqlClient>, admite la lectura y escritura en datos de FILESTREAM mediante la clase <xref:Microsoft.Data.SqlTypes.SqlFileStream> definida en el espacio de nombres <xref:System.Data.SqlTypes>. `SqlFileStream` hereda de la clase <xref:System.IO.Stream>, que proporciona métodos para leer y escribir en flujos de datos. Al leer de una secuencia, se transfieren datos de la secuencia a una estructura de datos, como una matriz de bytes. Al escribir, se transfieren los datos de la estructura de datos a una secuencia.

### <a name="creating-the-sql-server-table"></a>Crear la tabla SQL Server

Las instrucciones siguientes de Transact-SQL crean una tabla denominada Employees e insertan una fila de datos. Una vez que haya habilitado el almacenamiento de FILESTREAM, puede usar esta tabla junto con los ejemplos de código siguientes. Al final de este tema se encuentran los vínculos a los recursos de los Libros en pantalla de SQL Server.

```sql
CREATE TABLE employees
(
  EmployeeId INT  NOT NULL  PRIMARY KEY,
  Photo VARBINARY(MAX) FILESTREAM  NULL,
  RowGuid UNIQUEIDENTIFIER  NOT NULL  ROWGUIDCOL
  UNIQUE DEFAULT NEWID()
)
GO
Insert into employees
Values(1, 0x00, default)
GO
```

### <a name="example-reading-overwriting-and-inserting-filestream-data"></a>Ejemplo: leer, sobrescribir e insertar datos FILESTREAM

En el ejemplo siguiente se muestra cómo leer datos de un FILESTREAM. El código obtiene la ruta de acceso lógica al archivo, estableciendo el `FileAccess` en `Read` y el `FileOptions` en `SequentialScan`. A continuación, el código Lee los bytes de SqlFileStream en el búfer. Los bytes se escriben en la ventana de la consola.

En el ejemplo también se muestra cómo escribir datos en un FILESTREAM en el que se sobrescriben todos los datos existentes. El código obtiene la ruta de acceso lógica al archivo y crea el `SqlFileStream`, estableciendo el `FileAccess` en `Write` y el `FileOptions` en `SequentialScan`. Un solo byte se escribe en el `SqlFileStream`, reemplazando todos los datos del archivo.

En el ejemplo también se muestra cómo escribir datos en FILESTREAM mediante el método Seek para anexar datos al final del archivo. El código obtiene la ruta de acceso lógica al archivo y crea el `SqlFileStream`, estableciendo el `FileAccess` en `ReadWrite` y el `FileOptions` en `SequentialScan`. El código usa el método Seek para buscar el final del archivo, anexando un solo byte al archivo existente.

```csharp
using System;
using Microsoft.Data.SqlClient;
using System.Data.SqlTypes;
using System.Data;
using System.IO;

namespace FileStreamTest
{
    class Program
    {
        static void Main(string[] args)
        {
            SqlConnectionStringBuilder builder = new SqlConnectionStringBuilder("server=(local);integrated security=true;database=myDB");
            ReadFileStream(builder);
            OverwriteFileStream(builder);
            InsertFileStream(builder);

            Console.WriteLine("Done");
        }

        private static void ReadFileStream(SqlConnectionStringBuilder connStringBuilder)
        {
            using (SqlConnection connection = new SqlConnection(connStringBuilder.ToString()))
            {
                connection.Open();
                SqlCommand command = new SqlCommand("SELECT TOP(1) Photo.PathName(), GET_FILESTREAM_TRANSACTION_CONTEXT() FROM employees", connection);

                SqlTransaction tran = connection.BeginTransaction(IsolationLevel.ReadCommitted);
                command.Transaction = tran;

                using (SqlDataReader reader = command.ExecuteReader())
                {
                    while (reader.Read())
                    {
                        // Get the pointer for the file
                        string path = reader.GetString(0);
                        byte[] transactionContext = reader.GetSqlBytes(1).Buffer;

                        // Create the SqlFileStream
                        using (Stream fileStream = new SqlFileStream(path, transactionContext, FileAccess.Read, FileOptions.SequentialScan, allocationSize: 0))
                        {
                            // Read the contents as bytes and write them to the console
                            for (long index = 0; index < fileStream.Length; index++)
                            {
                                Console.WriteLine(fileStream.ReadByte());
                            }
                        }
                    }
                }
                tran.Commit();
            }
        }

        private static void OverwriteFileStream(SqlConnectionStringBuilder connStringBuilder)
        {
            using (SqlConnection connection = new SqlConnection(connStringBuilder.ToString()))
            {
                connection.Open();

                SqlCommand command = new SqlCommand("SELECT TOP(1) Photo.PathName(), GET_FILESTREAM_TRANSACTION_CONTEXT() FROM employees", connection);

                SqlTransaction tran = connection.BeginTransaction(IsolationLevel.ReadCommitted);
                command.Transaction = tran;

                using (SqlDataReader reader = command.ExecuteReader())
                {
                    while (reader.Read())
                    {
                        // Get the pointer for file
                        string path = reader.GetString(0);
                        byte[] transactionContext = reader.GetSqlBytes(1).Buffer;

                        // Create the SqlFileStream
                        using (Stream fileStream = new SqlFileStream(path, transactionContext, FileAccess.Write, FileOptions.SequentialScan, allocationSize: 0))
                        {
                            // Write a single byte to the file. This will
                            // replace any data in the file.
                            fileStream.WriteByte(0x01);
                        }
                    }
                }
                tran.Commit();
            }
        }

        private static void InsertFileStream(SqlConnectionStringBuilder connStringBuilder)
        {
            using (SqlConnection connection = new SqlConnection(connStringBuilder.ToString()))
            {
                connection.Open();

                SqlCommand command = new SqlCommand("SELECT TOP(1) Photo.PathName(), GET_FILESTREAM_TRANSACTION_CONTEXT() FROM employees", connection);

                SqlTransaction tran = connection.BeginTransaction(IsolationLevel.ReadCommitted);
                command.Transaction = tran;

                using (SqlDataReader reader = command.ExecuteReader())
                {
                    while (reader.Read())
                    {
                        // Get the pointer for file
                        string path = reader.GetString(0);
                        byte[] transactionContext = reader.GetSqlBytes(1).Buffer;

                        using (Stream fileStream = new SqlFileStream(path, transactionContext, FileAccess.ReadWrite, FileOptions.SequentialScan, allocationSize: 0))
                        {
                            // Seek to the end of the file
                            fileStream.Seek(0, SeekOrigin.End);

                            // Append a single byte
                            fileStream.WriteByte(0x01);
                        }
                    }
                }
                tran.Commit();
            }

        }
    }
}
```

Para obtener otro ejemplo, vea [Cómo almacenar y recuperar datos binarios en una columna de flujo de archivo](https://www.codeproject.com/Articles/32216/How-to-store-and-fetch-binary-data-into-a-file-str).

## <a name="resources-in-sql-server-books-online"></a>Recursos en Libros en pantalla de SQL Server

La documentación completa de FILESTREAM se encuentra en las secciones siguientes de los Libros en pantalla de SQL Server.

|Tema|Descripción|
|-----------|-----------------|
|[FILESTREAM (SQL Server)](../../../relational-databases/blob/filestream-sql-server.md)|Describe cuándo usar el almacenamiento de FILESTREAM y cómo integra el SQL Server Motor de base de datos con un sistema de archivos NTFS.|
|[Crear aplicaciones cliente para datos FILESTREAM](../../../relational-databases/blob/create-client-applications-for-filestream-data.md)|Describe las funciones de la API de Windows para trabajar con datos FILESTREAM.|
|[FILESTREAM y otras características de SQL Server](../../../relational-databases/blob/filestream-compatibility-with-other-sql-server-features.md)|Proporciona consideraciones, directrices y limitaciones para usar datos FILESTREAM con otras características de SQL Server.|

## <a name="next-steps"></a>Pasos siguientes
- [Tipos de datos de SQL Server en ADO.NET](sql-server-data-types.md)
- [Datos binarios y datos de valores grandes de SQL Server](sql-server-binary-large-value-data.md)
