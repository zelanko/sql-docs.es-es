---
title: "Procedimientos almacenados del sistema XML | Microsoft Docs"
ms.custom: ""
ms.date: "03/03/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-xml"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "procedimientos almacenados del sistema [SQL Server], XML"
  - "sp_xml_removedocument"
  - "Instrucción OPENXML, procedimientos almacenados del sistema"
  - "sp_xml_preparedocument"
  - "XML [SQL Server], procedimientos almacenados del sistema"
ms.assetid: e60c7f85-6823-4d28-93d6-b053d08cc830
caps.latest.revision: 27
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 27
---
# Procedimientos almacenados del sistema XML
  SQL Server proporciona los siguientes procedimientos almacenados que se utilizan junto con OPENXML:  
  
-   [sp_xml_preparedocument &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-xml-preparedocument-transact-sql.md)  
  
-   [sp_xml_removedocument &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-xml-removedocument-transact-sql.md)  
  
 Para escribir consultas con OPENXML, primero debe crear una representación interna del documento XML llamando a **sp_xml_preparedocument**. El procedimiento almacenado devuelve un identificador a la representación interna del documento XML. A continuación, este identificador se pasa a OPENXML. OPENXML ofrece vistas del conjunto de filas del documento basándose en XPaths. Concretamente, se trata de un patrón de filas y uno o varios patrones de columnas.  
  
> [!NOTE]  
>  El identificador de documentos devuelto por **sp_xml_preparedocument** es válido mientras dure la sesión.  
  
 La representación interna de un documento XML se puede quitar de la memoria llamando al procedimiento almacenado del sistema **sp_xml_removedocument**.  
  
## Vea también  
 [OPENXML &#40;Transact-SQL&#41;](../../t-sql/functions/openxml-transact-sql.md)   
 [OPENXML &#40;SQL Server&#41;](../../relational-databases/xml/openxml-sql-server.md)  
  
  