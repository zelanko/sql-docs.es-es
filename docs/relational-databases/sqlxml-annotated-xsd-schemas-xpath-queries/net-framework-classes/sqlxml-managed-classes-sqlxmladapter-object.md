---
title: Objeto SqlXmlAdapter (SQLXML)
description: Obtenga información sobre el objeto SqlXmlAdapter que proporciona métodos que facilitan la interacción con el conjunto de objetos en el .NET Framework.
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- void Update(DataSet ds) method
- SqlXmlAdapter object
- void Fill(DataSet ds) method
- SQLXML Managed Classes, SqlXmlAdapter object
- Managed Classes [SQLXML], SqlXmlAdapter object
ms.assetid: 0a16eddf-fc26-4d92-82d4-359b5fb905d5
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 77174c85a99bb441794248bcae0d5e50fcfa5055
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85773047"
---
# <a name="sqlxml-managed-classes---sqlxmladapter-object"></a>Clases administradas de SQLXML: objeto SqlXmlAdapter
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  Este objeto proporciona métodos que facilitan la interacción con el conjunto de datos de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework. Para obtener un ejemplo funcional, vea [obtener acceso a la funcionalidad de SQLXML en el entorno de .net](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/accessing-sqlxml-functionality-in-the-net-environment.md).  
  
 El objeto SqlXmlAdapter admite estos métodos:  
  
 void Fill (DataSet DS)  
 Rellena el conjunto de datos de .NET Framework con los datos XML recuperados de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 void Update (DataSet DS)  
 Aplica actualizaciones a los registros de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a partir de los datos del conjunto de datos.  
  
 El objeto SqlXmlAdapter admite estos constructores:  
  
```  
public SqlXmlAdapter(SqlXmlCommand  cmd)   
  
public SqlXmlAdapter(  
                     string commandText,   
                     SqlXmlCommandType cmdType,   
                     string connectionString  
                      )   
  
public SqlXmlAdapter(  
                     Stream commandStream,   
                     SqlXmlCommandType cmdType,   
                     string connectionString  
                     )   
```  
  
## <a name="see-also"></a>Consulte también  
 [Objeto SqlXmlCommand &#40;clases administradas de SQLXML&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/sqlxml-managed-classes-sqlxmlcommand-object.md)   
 [Objeto SqlXmlParameter &#40;clases administradas de SQLXML&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/sqlxml-managed-classes-sqlxmlparameter-object.md)  
  
  
