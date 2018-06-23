---
title: Procedimientos almacenados del sistema XML | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-xml
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- system stored procedures [SQL Server], XML
- sp_xml_removedocument
- OPENXML statement, system stored procedures
- sp_xml_preparedocument
- XML [SQL Server], system stored procedures
ms.assetid: e60c7f85-6823-4d28-93d6-b053d08cc830
caps.latest.revision: 26
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 6baa451df5a2e341b20130d163607d6bdcc5e924
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36109213"
---
# <a name="xml-system-stored-procedures"></a>Procedimientos almacenados del sistema XML
  SQL Server proporciona los siguientes procedimientos almacenados que se utilizan junto con OPENXML:  
  
-   [sp_xml_preparedocument &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-xml-preparedocument-transact-sql)  
  
-   [sp_xml_removedocument &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-xml-removedocument-transact-sql)  
  
 Para escribir consultas con OPENXML, primero debe crear una representación interna del documento XML llamando a **sp_xml_preparedocument**. El procedimiento almacenado devuelve un identificador a la representación interna del documento XML. A continuación, este identificador se pasa a OPENXML. OPENXML ofrece vistas del conjunto de filas del documento basándose en XPaths. Concretamente, se trata de un patrón de filas y uno o varios patrones de columnas.  
  
> [!NOTE]  
>  El identificador de documentos devuelto por **sp_xml_preparedocument** es válido mientras dure la sesión.  
  
 La representación interna de un documento XML se puede quitar de la memoria llamando al procedimiento almacenado del sistema **sp_xml_removedocument** .  
  
## <a name="see-also"></a>Vea también  
 [OPENXML &#40;Transact-SQL&#41;](/sql/t-sql/functions/openxml-transact-sql)   
 [OPENXML &#40;SQL Server&#41;](../xml/openxml-sql-server.md)  
  
  
