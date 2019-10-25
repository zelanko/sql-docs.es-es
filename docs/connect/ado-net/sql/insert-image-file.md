---
title: Inserción de una imagen desde un archivo
description: Describe cómo trabajar con una imagen de un archivo.
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 35900aa2-5615-4174-8212-ba184c6b82fb
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: d8f7b561a6aba4539964d73dacfd9e45db2dd6aa
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452173"
---
# <a name="inserting-an-image-from-a-file"></a>Inserción de una imagen desde un archivo

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[Descargar ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

Puede escribir un objeto binario grande (BLOB) en una base de datos como datos binarios o de caracteres, dependiendo del tipo de campo del origen de datos. BLOB es un término genérico que hace referencia a los tipos de datos `text`, `ntext` y `image`, que suelen contener documentos e imágenes.  
  
Para escribir un valor BLOB en la base de datos, emita la instrucción INSERT o UPDATE correspondiente y pase el valor BLOB como parámetro de entrada. Si el BLOB se almacena como texto, como un SQL Server campo `text`, puede pasar el BLOB como un parámetro de cadena. Si el BLOB se almacena en formato binario, como un SQL Server campo `image`, puede pasar una matriz de tipo `byte` como parámetro binario.
  
## <a name="example"></a>Ejemplo  
En el ejemplo de código siguiente se agrega información de empleado a la tabla Employees de la base de datos Northwind. Una foto del empleado se lee de un archivo y se agrega al campo Photo de la tabla, que es un campo de imagen.  
  
```csharp  
public static void AddEmployee(  
  string lastName,   
  string firstName,   
  string title,   
  DateTime hireDate,   
  int reportsTo,   
  string photoFilePath,   
  string connectionString)  
{  
  byte[] photo = GetPhoto(photoFilePath);  
  
  using (SqlConnection connection = new SqlConnection(  
    connectionString))  
  
  SqlCommand command = new SqlCommand(  
    "INSERT INTO Employees (LastName, FirstName, " +  
    "Title, HireDate, ReportsTo, Photo) " +  
    "Values(@LastName, @FirstName, @Title, " +  
    "@HireDate, @ReportsTo, @Photo)", connection);   
  
  command.Parameters.Add("@LastName",    
     SqlDbType.NVarChar, 20).Value = lastName;  
  command.Parameters.Add("@FirstName",   
      SqlDbType.NVarChar, 10).Value = firstName;  
  command.Parameters.Add("@Title",       
      SqlDbType.NVarChar, 30).Value = title;  
  command.Parameters.Add("@HireDate",   
       SqlDbType.DateTime).Value = hireDate;  
  command.Parameters.Add("@ReportsTo",   
      SqlDbType.Int).Value = reportsTo;  
  
  command.Parameters.Add("@Photo",  
      SqlDbType.Image, photo.Length).Value = photo;  
  
  connection.Open();  
  command.ExecuteNonQuery();  
  }  
}  
  
public static byte[] GetPhoto(string filePath)  
{  
  FileStream stream = new FileStream(  
      filePath, FileMode.Open, FileAccess.Read);  
  BinaryReader reader = new BinaryReader(stream);  
  
  byte[] photo = reader.ReadBytes((int)stream.Length);  
  
  reader.Close();  
  stream.Close();  
  
  return photo;  
}  
```  
  
## <a name="next-steps"></a>Pasos siguientes
- [Datos binarios y datos de valores grandes de SQL Server](sql-server-binary-large-value-data.md)
