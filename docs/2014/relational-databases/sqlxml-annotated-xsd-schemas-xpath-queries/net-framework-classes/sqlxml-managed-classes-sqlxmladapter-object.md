---
title: Objeto SqlXmlAdapter (clases administradas de SQLXML) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- void Update(DataSet ds) method
- SqlXmlAdapter object
- void Fill(DataSet ds) method
- SQLXML Managed Classes, SqlXmlAdapter object
- Managed Classes [SQLXML], SqlXmlAdapter object
ms.assetid: 0a16eddf-fc26-4d92-82d4-359b5fb905d5
caps.latest.revision: 22
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: d657ba49f7d4905eef8eaa0bdc3ca4327852df6d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36199290"
---
# <a name="sqlxmladapter-object-sqlxml-managed-classes"></a>Objeto SqlXmlAdapter (clases administradas SQLXML)
  Este objeto proporciona métodos que facilitan la interacción con el conjunto de datos de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework. Para obtener un ejemplo funcional, vea [obtiene acceso a la funcionalidad de SQLXML en el entorno .NET](accessing-sqlxml-functionality-in-the-net-environment.md).  
  
 El objeto SqlXmlAdapter admite estos métodos:  
  
 void Fill (DataSet ds)  
 Rellena el conjunto de datos de .NET Framework con los datos XML recuperados de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 void Update (DataSet ds)  
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
  
## <a name="see-also"></a>Vea también  
 [Objeto SqlXmlCommand &#40;clases administradas de SQLXML&#41;](sqlxml-4-0-net-framework-support-managed-classes.md)   
 [Objeto SqlXmlParameter &#40;clases administradas de SQLXML&#41;](sqlxml-managed-classes-sqlxmlparameter-object.md)  
  
  