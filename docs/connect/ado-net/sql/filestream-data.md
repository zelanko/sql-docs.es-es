---
title: Datos de FILESTREAM
description: Describe cómo trabajar con datos de valores grandes almacenados en SQL Server 2008 con el atributo FILESTREAM.
ms.date: 08/15/2019
ms.assetid: bd8b845c-0f09-4295-b466-97ef106eefa8
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: e3e26a76522d1c1a99794076c5f152e6ec1e1f7d
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "78896743"
---
# <a name="filestream-data"></a>Datos de FILESTREAM

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

El atributo de almacenamiento FILESTREAM sirve para los datos binarios (BLOB) almacenados en una columna varbinary(max). Antes de FILESTREAM, el almacenamiento de datos binarios requería un tratamiento especial. Los datos no estructurados, como los documentos de texto, las imágenes y el vídeo, se suelen almacenar fuera de la base de datos, por lo que resultan difíciles de administrar.

> [!NOTE]
> Debe instalar .NET Framework 3.5 SP1 (o posterior) o .NET Core para trabajar con datos de FILESTREAM mediante SqlClient.

La especificación del atributo FILESTREAM en una columna varbinary(max) provoca que SQL Server almacene los datos en el sistema de archivos NTFS local en lugar de hacerlo en el archivo de base de datos. Aunque se almacenan por separado, puede usar las mismas instrucciones de Transact-SQL admitidas para trabajar con los datos varbinary(max) almacenados en la base de datos.

## <a name="sqlclient-support-for-filestream"></a>Compatibilidad de SqlClient con FILESTREAM

El proveedor de datos SqlClient de Microsoft para SQL Server, <xref:Microsoft.Data.SqlClient>, admite la lectura y escritura en datos de FILESTREAM mediante la clase <xref:Microsoft.Data.SqlTypes.SqlFileStream> definida en el espacio de nombres <xref:System.Data.SqlTypes>. `SqlFileStream` hereda de la clase <xref:System.IO.Stream>, que proporciona métodos para leer y escribir en flujos de datos. Al leer de un flujo, se transfieren datos del flujo a una estructura de datos, como una matriz de bytes. Al escribir, se transfieren los datos de la estructura de datos a un flujo.

### <a name="creating-the-sql-server-table"></a>Creación de la tabla de SQL Server

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

### <a name="example-reading-overwriting-and-inserting-filestream-data"></a>Ejemplo: Lectura, sobrescritura e inserción de datos FILESTREAM

El ejemplo siguiente muestra cómo se leen datos de FILESTREAM. El código obtiene la ruta de acceso lógica al archivo, estableciendo `FileAccess` en `Read` y `FileOptions` en `SequentialScan`. A continuación, el código lee los bytes de SqlFileStream en el búfer. Los bytes se escriben luego en la ventana de la consola.

El ejemplo muestra también cómo se escriben datos en una instancia de FILESTREAM en la que se sobrescriben todos los datos existentes. El código obtiene la ruta de acceso lógica al archivo y crea `SqlFileStream`, estableciendo `FileAccess` en `Write` y `FileOptions` en `SequentialScan`. Un solo byte se escribe en `SqlFileStream`, reemplazando todos los datos del archivo.

En el ejemplo también se muestra cómo escribir datos en FILESTREAM mediante el método Seek para anexar datos al final del archivo. El código obtiene la ruta de acceso lógica al archivo y crea `SqlFileStream`, estableciendo `FileAccess` en `ReadWrite` y `FileOptions` en `SequentialScan`. El código usa el método Seek para buscar el final del archivo, anexando un solo byte al archivo existente.

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

## <a name="resources-in-sql-server-books-online"></a>Recursos en los Libros en pantalla de SQL Server

La documentación completa de FILESTREAM se encuentra en las secciones siguientes de los Libros en pantalla de SQL Server.

|Tema|Descripción|
|-----------|-----------------|
|[FILESTREAM (SQL Server)](../../../relational-databases/blob/filestream-sql-server.md)|Describe cuándo usar el almacenamiento de FILESTREAM y cómo se integra el motor de base de datos de SQL Server con un sistema de archivos NTFS.|
|[Crear aplicaciones cliente para datos FILESTREAM](../../../relational-databases/blob/create-client-applications-for-filestream-data.md)|Describe las funciones de la API de Windows para trabajar con datos FILESTREAM.|
|[FILESTREAM y otras características de SQL Server](../../../relational-databases/blob/filestream-compatibility-with-other-sql-server-features.md)|Proporciona consideraciones, directrices y limitaciones para usar datos FILESTREAM con otras características de SQL Server.|

## <a name="next-steps"></a>Pasos siguientes
- [Tipos de datos de SQL Server en ADO.NET](sql-server-data-types.md)
- [Datos binarios y datos de valores grandes de SQL Server](sql-server-binary-large-value-data.md)
