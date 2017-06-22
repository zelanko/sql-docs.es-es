---
title: "Códigos de retorno e información de error de automatización OLE | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-ole
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- return codes [SQL Server]
- OLE Automation [SQL Server], return codes
- OLE Automation [SQL Server], errors
ms.assetid: 9696fb05-e9e8-4836-b359-d4de0be0eeb2
caps.latest.revision: 22
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b1a64e9ca8e9999411edf97c76c50f577790af27
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="ole-automation-return-codes-and-error-information"></a>Códigos de retorno e información de error de automatización OLE
  Los procedimientos almacenados del sistema de automatización OLE devuelven un código de retorno **int** que es el HRESULT devuelto por la operación de automatización OLE subyacente. Un HRESULT con el valor 0 indica que la operación se realizó correctamente. Un valor de HRESULT distinto de cero es un código de error OLE con formato hexadecimal 0x800*nnnnn*, aunque cuando se devuelve como un valor **int** en un código de retorno de un procedimiento almacenado, tiene el formato 214*nnnnnnn*.  
  
 Por ejemplo, pasar un nombre de objeto no válido (SQLDMO.Xyzzy) a sp_OACreate hace que el procedimiento devuelva un HRESULT **int** de 2147221005, que es 0x800401f3 en formato hexadecimal.  
  
 Puede usar `CONVERT(binary(4), @hresult)` para convertir un HRESULT **int** en un valor **binary** . Sin embargo, el uso de `CONVERT(char(10), CONVERT(binary(4), @hresult))` da como resultado una cadena ilegible, porque cada byte de HRESULT se convierte en un carácter ASCII. Puede usar el siguiente procedimiento almacenado HexToChar como ejemplo para convertir un HRESULT **int** a un valor **char** que contenga una cadena hexadecimal legible.  
  
```  
USE AdventureWorks2012;  
GO  
IF EXISTS(SELECT name FROM sys.objects  
          WHERE name = N'dbo.sp_HexToChar')  
    DROP PROCEDURE HexToChar;  
GO  
CREATE PROCEDURE dbo.sp_HexToChar  
    @BinValue varbinary(255),  
    @HexCharValue nvarchar(255) OUTPUT  
AS  
    DECLARE @CharValue nvarchar(255);  
    DECLARE @Position int;  
    DECLARE @Length int;  
    DECLARE @HexString nchar(16);  
    SELECT @CharValue = N'0x';  
    SELECT @Position = 1;  
    SELECT @Length = DATALENGTH(@BinValue);  
    SELECT @HexString = N'0123456789ABCDEF';  
    WHILE (@Position <= @Length)  
    BEGIN  
        DECLARE @TempInt int;  
        DECLARE @FirstInt int;  
        DECLARE @SecondInt int;  
        SELECT @TempInt = CONVERT(int, SUBSTRING(@BinValue,@Position,1));  
        SELECT @FirstInt = FLOOR(@TempInt/16);  
        SELECT @SecondInt = @TempInt - (@FirstInt*16);  
        SELECT @CharValue = @CharValue +  
            SUBSTRING(@HexString, @FirstInt+1, 1) +  
            SUBSTRING(@HexString, @SecondInt+1, 1);  
        SELECT @Position = @Position + 1;  
    END  
    SELECT @HexCharValue = @CharValue;  
GO  
DECLARE @BinVariable varbinary(35);  
DECLARE @CharValue nvarchar(35);  
  
SET @BinVariable = 123456;  
  
EXECUTE dbo.sp_HexToChar  
    @binvalue = @BinVariable,  
    @HexCharValue = @CharValue OUTPUT;  
  
SELECT @BinVariable AS BinaryValue,  
    @CharValue AS CharacterRep;  
GO  
```  
  
 Puede usar el siguiente ejemplo de procedimiento almacenado, **sp_displayoaerrorinfo** , para mostrar información de errores de automatización OLE cuando alguno de los procedimientos de automatización OLE devuelva un código de retorno HRESULT distinto de cero. En este ejemplo de procedimiento almacenado se usa **HexToChar**.  
  
```  
CREATE PROCEDURE dbo.sp_DisplayOAErrorInfo  
    @Object int,  
    @HResult int  
AS  
    DECLARE @Output nvarchar(255);  
    DECLARE @HRHex nchar(10);  
    DECLARE @HR int;  
    DECLARE @Source nvarchar(255);  
    DECLARE @Description nvarchar(255);  
    PRINT N'OLE Automation Error Information';  
    EXEC HexToChar @HResult, @HRHex OUT;  
    SELECT @Output = N'  HRESULT: ' + @HRHex;  
    PRINT @Output;  
    EXEC @HR = sp_OAGetErrorInfo  
        @Object,  
        @Source OUT,  
        @Description OUT;  
    IF @HR = 0  
    BEGIN  
        SELECT @Output = N'  Source: ' + @Source;  
        PRINT @Output;  
        SELECT @Output = N'  Description: '  
               + @Description;  
        PRINT @Output;  
    END  
    ELSE  
    BEGIN  
       PRINT N' sp_OAGetErrorInfo failed.';  
       RETURN;  
    END  
GO  
```  
  
## <a name="related-content"></a>Contenido relacionado  
 [sp_OAGetErrorInfo &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-oageterrorinfo-transact-sql.md)  
  
  
