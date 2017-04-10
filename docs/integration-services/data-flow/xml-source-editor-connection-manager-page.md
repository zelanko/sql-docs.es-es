---
title: "Editor de origen de XML (p&#225;gina Administrador de conexiones) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.xmlsourceadapter.connectionmanager.f1"
helpviewer_keywords: 
  - "Editor de origen de XML"
ms.assetid: e6507403-a3ce-4b6f-91fc-a7de9f7b6283
caps.latest.revision: 20
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 20
---
# Editor de origen de XML (p&#225;gina Administrador de conexiones)
  Utilice la página **Administrador de conexiones** del **Editor de origen de XML** para especificar un archivo XML y el XSD que transforma los datos XML.  
  
 Para obtener más información acerca del origen XML, vea [XML Source](../../integration-services/data-flow/xml-source.md).  
  
## Opciones estáticas  
 **Modo de acceso a datos**  
 Especifique el método para seleccionar datos del origen.  
  
|Value|Description|  
|-----------|-----------------|  
|Ubicación del archivo XML|Recupera datos de un archivo XML.|  
|Archivo XML de variable|Especifica el nombre de archivo XML en una variable.<br /><br /> **Información relacionada**: [Usar variables en paquetes](../Topic/Use%20Variables%20in%20Packages.md)|  
|Datos XML de variable|Recupera datos XML de una variable.|  
  
 **Utilizar esquema insertado**  
 Especifique si los datos de origen XML contienen el esquema XSD que define y valida su estructura y sus datos.  
  
 **Ubicación de XSD**  
 Especifique la ruta de acceso y el nombre de archivo del archivo de esquema XSD, o busque el archivo haciendo clic en **Examinar**.  
  
 **Examinar**  
 Use el cuadro de diálogo **Abrir** para buscar el archivo de esquema XSD.  
  
 **Generar XSD**  
 Use el cuadro de diálogo **Guardar como** para seleccionar una ubicación para el archivo de esquema XSD generado automáticamente. El editor deduce el esquema de la estructura de los datos XML.  
  
## Opciones dinámicas del modo de acceso a datos  
  
### Modo de acceso a datos = Ubicación del archivo XML  
 **Ubicación de XML**  
 Especifique la ruta de acceso y el nombre de archivo del archivo de datos XML, o busque el archivo haciendo clic en **Examinar**.  
  
 **Examinar**  
 Use el cuadro de diálogo **Abrir** para buscar el archivo de datos XML.  
  
### Modo de acceso a datos = Datos XML de variable  
 **Nombre de variable**  
 Seleccione la variable que contiene la ruta de acceso y el nombre del archivo XML.  
  
### Modo de acceso a datos = Datos XML de variable  
 **Nombre de variable**  
 Seleccione la variable que contiene los datos XML.  
  
## Vea también  
 [Referencia de errores y mensajes de Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Editor de origen de XML &#40;página Columnas&#41;](../../integration-services/data-flow/xml-source-editor-columns-page.md)   
 [Editor de origen de XML &#40;página Salida de error&#41;](../../integration-services/data-flow/xml-source-editor-error-output-page.md)   
 [Extraer datos mediante el origen de XML](../../integration-services/data-flow/extract-data-by-using-the-xml-source.md)  
  
  