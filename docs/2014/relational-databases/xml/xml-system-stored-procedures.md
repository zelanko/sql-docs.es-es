---
title: Procedimientos almacenados del sistema XML | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- system stored procedures [SQL Server], XML
- sp_xml_removedocument
- OPENXML statement, system stored procedures
- sp_xml_preparedocument
- XML [SQL Server], system stored procedures
ms.assetid: e60c7f85-6823-4d28-93d6-b053d08cc830
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 20ea97f50592c6d8abc51e64acb4a164ad0b95b3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "63192971"
---
# <a name="xml-system-stored-procedures"></a>Procedimientos almacenados del sistema XML
  SQL Server proporciona los siguientes procedimientos almacenados que se utilizan junto con OPENXML:  
  
-   [sp_xml_preparedocument &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-xml-preparedocument-transact-sql)  
  
-   [sp_xml_removedocument &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-xml-removedocument-transact-sql)  
  
 Para escribir consultas con OPENXML, primero debe crear una representación interna del documento XML llamando a **sp_xml_preparedocument**. El procedimiento almacenado devuelve un identificador a la representación interna del documento XML. A continuación, este identificador se pasa a OPENXML. OPENXML ofrece vistas del conjunto de filas del documento basándose en XPaths. Concretamente, se trata de un patrón de filas y uno o varios patrones de columnas.  
  
> [!NOTE]  
>  El identificador de documentos devuelto por **sp_xml_preparedocument** es válido mientras dure la sesión.  
  
 La representación interna de un documento XML se puede quitar de la memoria llamando al procedimiento almacenado del sistema **sp_xml_removedocument** .  
  
## <a name="see-also"></a>Consulte también  
 [OPENXML &#40;Transact-SQL&#41;](/sql/t-sql/functions/openxml-transact-sql)   
 [OPENXML &#40;SQL Server&#41;](../xml/openxml-sql-server.md)  
  
  
