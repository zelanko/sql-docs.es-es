---
title: Códigos de retorno e información de error de automatización OLE | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-ole
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- return codes [SQL Server]
- OLE Automation [SQL Server], return codes
- OLE Automation [SQL Server], errors
ms.assetid: 9696fb05-e9e8-4836-b359-d4de0be0eeb2
caps.latest.revision: 22
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 782655aa435ba69a38f4de1d854c1ff9837a6778
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36203370"
---
# <a name="ole-automation-return-codes-and-error-information"></a>Códigos de retorno e información de error de OLE Automation
  Los procedimientos almacenados del sistema de OLE Automation devuelven un código de retorno `int` que es el HRESULT devuelto por la operación de OLE Automation subyacente. Un HRESULT con el valor 0 indica que la operación se realizó correctamente. Un valor de HRESULT distinto de cero es un código de error OLE de formato hexadecimal 0 x 800*nnnnn*, pero cuando se devuelve como un `int` valor en un código de retorno de procedimiento almacenado, HRESULT no tiene el formato 214*nnnnnnn*.  
  
 Por ejemplo, si se pasa un nombre de objeto no válido (SQLDMO. (Xyzzy) a sp_OACreate hace que el procedimiento devuelva un `int` HRESULT de 2147221005, que es 0x800401f3 en formato hexadecimal.  
  
 Puede utilizar `CONVERT(binary(4), @hresult)` para convertir un HRESULT `int` en un valor `binary`. Sin embargo, el uso de `CONVERT(char(10), CONVERT(binary(4), @hresult))` da como resultado una cadena ilegible, porque cada byte de HRESULT se convierte en un carácter ASCII. Puede utilizar el siguiente procedimiento almacenado hextochar como de ejemplo para convertir un `int` HRESULT a un `char` valor que contiene una cadena hexadecimal legible.  
  
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
  
 Puede usar el siguiente ejemplo de procedimiento almacenado, **sp_displayoaerrorinfo** , para mostrar información de errores de automatización OLE cuando alguno de los procedimientos de automatización OLE devuelva un código de retorno HRESULT distinto de cero. Este ejemplo de procedimiento almacenado se usa `HexToChar`.  
  
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
 [sp_OAGetErrorInfo &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-oageterrorinfo-transact-sql)  
  
  
