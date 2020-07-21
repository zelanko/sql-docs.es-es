---
title: Objeto SqlXmlAdapter (clases administradas de SQLXML) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
author: rothja
ms.author: jroth
ms.openlocfilehash: f950ad2bd22fa84b5f62711ee4fd290ebab136bb
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85015300"
---
# <a name="sqlxmladapter-object-sqlxml-managed-classes"></a>Objeto SqlXmlAdapter (clases administradas SQLXML)
  Este objeto proporciona métodos que facilitan la interacción con el conjunto de datos de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework. Para obtener un ejemplo funcional, vea [obtener acceso a la funcionalidad de SQLXML en el entorno de .net](accessing-sqlxml-functionality-in-the-net-environment.md).  
  
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
 [Objeto SqlXmlCommand &#40;clases administradas de SQLXML&#41;](sqlxml-4-0-net-framework-support-managed-classes.md)   
 [Objeto SqlXmlParameter &#40;clases administradas de SQLXML&#41;](sqlxml-managed-classes-sqlxmlparameter-object.md)  
  
  
