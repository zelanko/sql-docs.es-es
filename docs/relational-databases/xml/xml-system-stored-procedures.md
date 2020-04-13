---
title: Procedimientos almacenados del sistema XML | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
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
ms.openlocfilehash: b39e3fef3b3729f9f2d4e58fe29e303d3070cb64
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/04/2020
ms.locfileid: "80664863"
---
# <a name="xml-system-stored-procedures"></a>Procedimientos almacenados del sistema XML
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  SQL Server proporciona los siguientes procedimientos almacenados que se utilizan junto con OPENXML:  
  
-   [sp_xml_preparedocument &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-xml-preparedocument-transact-sql.md)  
  
-   [sp_xml_removedocument &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-xml-removedocument-transact-sql.md)  
  
 Para escribir consultas con OPENXML, primero debe crear una representación interna del documento XML llamando a **sp_xml_preparedocument**. El procedimiento almacenado devuelve un identificador a la representación interna del documento XML. A continuación, este identificador se pasa a OPENXML. OPENXML ofrece vistas del conjunto de filas del documento basándose en XPaths. Concretamente, se trata de un patrón de filas y uno o varios patrones de columnas.  
  
> [!NOTE]  
>  El identificador de documentos devuelto por **sp_xml_preparedocument** es válido mientras dure la sesión.  
  
 La representación interna de un documento XML se puede quitar de la memoria llamando al procedimiento almacenado del sistema **sp_xml_removedocument** .  
  
## <a name="see-also"></a>Consulte también  
 [OPENXML &#40;Transact-SQL&#41;](../../t-sql/functions/openxml-transact-sql.md)   
 [OPENXML &#40;SQL Server&#41;](../../relational-databases/xml/openxml-sql-server.md)  
  
  
