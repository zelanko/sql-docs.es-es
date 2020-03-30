---
title: xml (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- xml_TSQL
- xml
dev_langs:
- TSQL
helpviewer_keywords:
- xml data type [SQL Server], about xml data type
ms.assetid: 9198f671-8e61-4ca4-9c3a-859f84020e62
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d8d863a6ca6a44a323c05f26298c68de774dfc3b
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "67948031"
---
# <a name="xml-transact-sql"></a>xml (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Es el tipo de datos que almacena datos de XML. Puede almacenar instancias de **xml** en una columna o una variable de tipo **xml**.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
xml ( [ CONTENT | DOCUMENT ] xml_schema_collection )  
```  
  
## <a name="arguments"></a>Argumentos  
 CONTENT  
 Restringe la instancia de **xml** a un fragmento de XML correcto. Los datos XML pueden contener cero o más elementos en el nivel superior. También se admiten nodos de texto en el nivel superior.  
  
 Este es el comportamiento predeterminado.  
  
 DOCUMENT  
 Restringe la instancia de **xml** a un documento de XML correcto. Los datos XML deben tener un elemento raíz (solo uno). No se admiten nodos de texto en el nivel superior.  
  
 *xml_schema_collection*  
 Es el nombre de una colección de esquemas XML. Para crear una columna o una variable **xml** con tipo, puede especificar opcionalmente el nombre de la colección de esquemas XML. Para obtener más información sobre XML con y sin tipo, vea [Comparar XML con tipo y XML sin tipo](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md).  
  
## <a name="remarks"></a>Observaciones  
 La representación almacenada de las instancias del tipo de datos **xml** no puede superar 2 gigabytes (GB) de tamaño.  
  
 Las facetas CONTENT y DOCUMENT solo se aplican a XML con tipo. Para obtener más información, vea [Comparar XML con tipo y XML sin tipo](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md).  
  
## <a name="examples"></a>Ejemplos  
  
```  
USE AdventureWorks;  
GO  
DECLARE @DemographicData xml (Person.IndividualSurveySchemaCollection);  
SET @DemographicData =  (SELECT TOP 1 Demographics FROM Person.Person);  
SELECT @DemographicData;  
GO  
```  
  
## <a name="see-also"></a>Consulte también  
 [Conversión de tipos de datos &#40;motor de base de datos&#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)   
 [Tipos de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [métodos del tipo de datos xml](../../t-sql/xml/xml-data-type-methods.md)   
 [Referencia del lenguaje XQuery &#40;SQL Server&#41;](../../xquery/xquery-language-reference-sql-server.md)  
  
  
