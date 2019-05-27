---
title: Editor de origen XML (página Administrador de conexiones) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.xmlsourceadapter.connectionmanager.f1
helpviewer_keywords:
- XML Source Editor
ms.assetid: e6507403-a3ce-4b6f-91fc-a7de9f7b6283
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 5965c48f91387944f223e1d0cfe666b19aba0e63
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66054297"
---
# <a name="xml-source-editor-connection-manager-page"></a>Editor de origen de XML (página Administrador de conexiones)
  Utilice la página **Administrador de conexiones** del **Editor de origen de XML** para especificar un archivo XML y el XSD que transforma los datos XML.  
  
 Para obtener más información acerca del origen XML, vea [XML Source](data-flow/xml-source.md).  
  
## <a name="static-options"></a>Opciones estáticas  
 **Modo de acceso a datos**  
 Especifique el método para seleccionar datos del origen.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|Ubicación del archivo XML|Recupera datos de un archivo XML.|  
|Archivo XML de variable|Especifica el nombre de archivo XML en una variable.<br /><br /> **Información relacionada**: [Usar variables en paquetes](../../2014/integration-services/use-variables-in-packages.md)|  
|Datos XML de variable|Recupera datos XML de una variable.|  
  
 **Utilizar esquema insertado**  
 Especifique si los datos de origen XML contienen el esquema XSD que define y valida su estructura y sus datos.  
  
 **Ubicación de XSD**  
 Especifique la ruta de acceso y el nombre de archivo del archivo de esquema XSD, o busque el archivo haciendo clic en **Examinar**.  
  
 **Examinar**  
 Use el cuadro de diálogo **Abrir** para buscar el archivo de esquema XSD.  
  
 **Generar XSD**  
 Use el cuadro de diálogo **Guardar como** para seleccionar una ubicación para el archivo de esquema XSD generado automáticamente. El editor deduce el esquema de la estructura de los datos XML.  
  
## <a name="data-access-mode-dynamic-options"></a>Opciones dinámicas del modo de acceso a datos  
  
### <a name="data-access-mode--xml-file-location"></a>Modo de acceso a datos = Ubicación del archivo XML  
 **Ubicación de XML**  
 Especifique la ruta de acceso y el nombre de archivo del archivo de datos XML, o busque el archivo haciendo clic en **Examinar**.  
  
 **Examinar**  
 Use el cuadro de diálogo **Abrir** para buscar el archivo de datos XML.  
  
### <a name="data-access-mode--xml-file-from-variable"></a>Modo de acceso a datos = Datos XML de variable  
 **Nombre de variable**  
 Seleccione la variable que contiene la ruta de acceso y el nombre del archivo XML.  
  
### <a name="data-access-mode--xml-data-from-variable"></a>Modo de acceso a datos = Datos XML de variable  
 **Nombre de variable**  
 Seleccione la variable que contiene los datos XML.  
  
## <a name="see-also"></a>Vea también  
 [Referencia de errores y mensajes de Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor de origen de XML &#40;página Columnas&#41;](../../2014/integration-services/xml-source-editor-columns-page.md)   
 [Editor de origen de XML &#40;página Salida de error&#41;](../../2014/integration-services/xml-source-editor-error-output-page.md)   
 [Extraer datos mediante el origen de XML](data-flow/extract-data-by-using-the-xml-source.md)  
  
  
