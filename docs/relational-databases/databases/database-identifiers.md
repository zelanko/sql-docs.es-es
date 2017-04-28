---
title: Identificadores de base de datos | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- TSQL
helpviewer_keywords:
- regular identifiers [SQL Server]
- identifiers [SQL Server]
- names [SQL Server], identifiers
- identifiers [SQL Server], about identifiers
- SQL Server identifiers
- Transact-SQL identifiers
- database objects [SQL Server], names
ms.assetid: 171291bb-f57f-4ad1-8cea-0b092d5d150c
caps.latest.revision: 40
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a6ec8d756aa5aa0c728ba5a3456a30809b4a0484
ms.lasthandoff: 04/11/2017

---
# <a name="database-identifiers"></a>Identificadores de base de datos
  El nombre de un objeto de base de datos se conoce como su identificador. Cualquier elemento de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede tener un identificador. Servidores, bases de datos y objetos de bases de datos, como tablas, vistas, columnas, índices, desencadenadores, procedimientos, restricciones, reglas, etc. pueden tener identificadores. Se requiere que la mayor parte de los objetos tengan identificadores; pero para ciertos objetos, como las restricciones, son opcionales.  
  
 El identificador de un objeto se crea cuando se define el objeto. A continuación, el identificador se utiliza para hacer referencia al objeto. Por ejemplo, la instrucción siguiente crea una tabla con el identificador `TableX`y dos columnas con los identificadores `KeyCol` y `Description`:  
  
```  
CREATE TABLE TableX  
(KeyCol INT PRIMARY KEY, Description nvarchar(80))  
```  
  
 Esta tabla tiene también una restricción sin nombre. La restricción `PRIMARY KEY` no tiene ningún identificador.  
  
 La intercalación de un identificador depende del nivel en que está definido. Se asigna a los identificadores de objetos de instancia, como los inicios de sesión y los nombres de base de datos, la intercalación predeterminada de la instancia. A los identificadores de objetos de una base de datos, como nombres de tablas, vistas y columnas, se asigna la intercalación predeterminada de la base de datos. Por ejemplo, es posible crear dos tablas con nombres que solo se diferencian en las mayúsculas en una base de datos con intercalación que distinga entre mayúsculas y minúsculas, pero no se pueden crear en una base de datos con intercalación que no distinga entre mayúsculas y minúsculas.  
  
> [!NOTE]  
>  Los nombres de variables o los parámetros de funciones y procedimientos almacenados deben cumplir las reglas para los identificadores de [!INCLUDE[tsql](../../includes/tsql-md.md)] .  
  
## <a name="classes-of-identifiers"></a>Clases de identificadores  
 Existen dos clases de identificadores:  
  
 Identificadores normales  
 Siguen las reglas de formato de los identificadores. Los identificadores normales no están delimitados cuando se usan en instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] .  
  
```  
SELECT *  
FROM TableX  
WHERE KeyCol = 124  
```  
  
 Identificadores delimitados  
 Se incluyen entre comillas dobles (") o corchetes ([ ]). Los identificadores que siguen las reglas de formato de los identificadores pueden no estar delimitados. Por ejemplo:  
  
```  
SELECT *  
FROM [TableX]         --Delimiter is optional.  
WHERE [KeyCol] = 124  --Delimiter is optional.  
```  
  
 Los identificadores que no cumplen las reglas de los identificadores deben estar delimitados en las instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] . Por ejemplo:  
  
```  
SELECT *  
FROM [My Table]      --Identifier contains a space and uses a reserved keyword.  
WHERE [order] = 10   --Identifier is a reserved keyword.  
```  
  
 Ambos identificadores, normales y delimitados, deben tener entre 1 y 128 caracteres. En el caso de las tablas temporales locales, el identificador puede tener un máximo de 116 caracteres.  
  
## <a name="rules-for-regular-identifiers"></a>Reglas de los identificadores normales  
 Los nombres de variables, funciones y procedimientos almacenados deben cumplir las siguientes reglas para los identificadores de [!INCLUDE[tsql](../../includes/tsql-md.md)] .  
  
1.  El primer carácter debe ser alguno de los siguientes:  
  
    -   Una letra, tal como se define en el estándar Unicode 3,2. La definición Unicode de letras incluye los caracteres latinos de la “a” a la “z” y de la “A” a la “Z”, además de los caracteres de letras de otros idiomas.  
  
    -   El signo de subrayado (_), arroba (@) o número (#).  
  
         Ciertos símbolos al principio de un identificador tienen un significado especial en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Un identificador normal que comience por el signo arroba siempre denotará una variable local o un parámetro, y no se puede usar como nombre de ningún otro tipo de objeto. Un identificador que empieza con el signo de número indica una tabla o procedimiento temporal. Un identificador que empieza con un signo de número doble (##) indica un objeto temporal global. Aunque es posible utilizar los caracteres de signo de número o doble signo de número para comenzar los nombres de otros tipos de objetos, no se recomienda hacerlo.  
  
         Algunas funciones de [!INCLUDE[tsql](../../includes/tsql-md.md)] tienen nombres que empiezan con un doble signo de arroba (@@). Para evitar confusiones con estas funciones, se recomienda no utilizar nombres que empiecen con @@.  
  
2.  Los caracteres subsiguientes pueden ser:  
  
    -   Letras, tal como se definen en el estándar Unicode 3,2.  
  
    -   Números decimales del alfabeto Latín básico u otros alfabetos de otros idiomas.  
  
    -   El signo de arroba, dólar ($), número o subrayado.  
  
3.  El identificador no debe ser una palabra reservada de [!INCLUDE[tsql](../../includes/tsql-md.md)] . [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se reserva las versiones en mayúsculas y minúsculas de las palabras reservadas. Cuando se utilizan en instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] , los identificadores que no cumplan estas reglas deben aparecer delimitados por comillas dobles o corchetes. Las palabras reservadas dependen del nivel de compatibilidad de la base de datos. Este nivel se puede establecer mediante la instrucción [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md) .  
  
4.  No se permiten los caracteres especiales o los espacios incrustados.  
  
5.  Los caracteres complementarios no están permitidos.  
  
 Cuando se utilizan en instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] , los identificadores que no cumplan estas reglas deben aparecer delimitados por comillas dobles o corchetes.  
  
> [!NOTE]  
>  Algunas reglas de formato de los identificadores normales dependen del nivel de compatibilidad de la base de datos. Este nivel se puede establecer mediante [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md).  
  
## <a name="see-also"></a>Vea también  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [CREATE DATABASE &#40;Transact-SQL de SQL Server&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [CREATE DEFAULT &#40;Transact-SQL&#41;](../../t-sql/statements/create-default-transact-sql.md)   
 [CREATE PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)   
 [CREATE RULE &#40;Transact-SQL&#41;](../../t-sql/statements/create-rule-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [CREATE VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/create-view-transact-sql.md)   
 [DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)   
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [Palabras clave reservadas &#40;Transact-SQL&#41;](../../t-sql/language-elements/reserved-keywords-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)  
  
  
