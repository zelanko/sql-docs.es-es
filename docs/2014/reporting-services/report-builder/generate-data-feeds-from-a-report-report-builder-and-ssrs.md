---
title: Generar fuentes de distribución de datos a partir de un informe (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: e68baae2-9f2a-4f13-9179-9ac7f29111c5
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ceca9ef914afeab3420bbd35c46c582c112644dc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66107848"
---
# <a name="generate-data-feeds-from-a-report-report-builder-and-ssrs"></a>Generar fuentes de distribución de datos a partir de un informe (Generador de informes y SSRS)
  Puede generar fuentes de datos compatibles con Atom a partir de informes y, a continuación, utilizar las fuentes de datos en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] aplicaciones, como el cliente, que pueden consumir fuentes de datos.  
  
 La extensión de representación de Atom de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] genera un documento de servicio de Atom que enumera las fuentes de distribución de datos disponibles en un informe. El documento enumera al menos una fuente de distribución de datos para cada región de datos del informe. Según el tipo de región de datos y los datos que esta muestra, [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] podría generar varias fuentes de distribución de datos a partir de una región de datos.  
  
 El documento de servicio de Atom contiene un identificador único para cada una de las fuentes de distribución de datos que se usa en una dirección URL para ver el contenido de la fuente de distribución de datos.  
  
 Para obtener más información, vea [Generar fuentes de distribución de datos a partir de informes &#40;Generador de informes y SSRS&#41;](generating-data-feeds-from-reports-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-generate-an-atom-service-document"></a>Generar un documento de servicio de Atom  
  
1.  En la página **Inicio** del Administrador de informes, navegue hasta el informe con el que desea generar las fuentes de distribución de datos.  
  
2.  Haga clic en el informe.  
  
     El informe se ejecuta.  
  
3.  En la barra de herramientas, haga clic en el icono Exportar a fuente de distribución de datos.  
  
     Aparece un mensaje en el que se pregunta si desea guardar o abrir el documento de Atom que contiene la fuente de distribución de datos.  
  
4.  Haga clic en **Guardar** para guardar el documento en el sistema de archivos o en **Abrir** para ver el contenido del documento antes de guardarlo. **De forma predeterminada, el documento se abre en un explorador.**  
  
5.  Busque la ubicación para guardar el documento.  
  
6.  Si lo desea, cambie el nombre del documento.  
  
    > [!NOTE]  
    >  De manera predeterminada, el nombre del documento es el del informe.  
  
7.  Compruebe que el tipo de documento es **Archivo ATOMSVC**y, a continuación, haga clic en **Guardar**.  
  
8.  Si lo desea, abra el archivo .atomsvc en un explorador o un editor de texto o XML.  
  
### <a name="to-view-an-atom-compliant-data-feed"></a>Ver una fuente de distribución de datos conforme a Atom  
  
1.  Si el documento de servicio de Atom no está abierto aún, búsquelo y ábralo en un explorador como Internet Explorer.  
  
2.  Copie la dirección URL de la fuente de distribución de datos que desea ver del documento de servicio de Atom al explorador.  
  
     El formato de la dirección URL es el siguiente:  
  
 `http://<server name>/ReportServer?%2f<ReportName>rs%3aCommand=Render&rs%3aFormat=ATOM&rc%3aDataFeed=<Identifier>`  
  
1.  Presione ENTRAR.  
  
     Aparece un mensaje en el que se pregunta si desea guardar o abrir el documento de Atom que contiene la fuente de distribución de datos.  
  
2.  Haga clic en **Guardar** para guardar el documento en el sistema de archivos, o en **Abrir** para ver la fuente de distribución de datos antes de guardar.  
  
3.  Busque la ubicación para guardar el documento.  
  
4.  Si lo desea, cambie el nombre del documento.  
  
    > [!NOTE]  
    >  De forma predeterminada, el nombre del documento es el del informe. Si el documento de servicio de Atom tiene varias fuentes, de forma predeterminada todas usas el mismo nombre, el del informe. Para diferenciarlas, cambie su nombre por otro descriptivo.  
  
5.  Compruebe que el tipo de documento es **Archivo ATOM**y, a continuación, haga clic en **Guardar**.  
  
6.  Si lo desea, abra el archivo .atom en un explorador o editor de texto o XML.  
  
## <a name="see-also"></a>Consulte también  
 [Exportar informes &#40;Generador de informes y SSRS&#41;](export-reports-report-builder-and-ssrs.md)  
  
  
