---
title: Exportar un dominio a un archivo .dqs | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.suite: sql
ms.technology:
- data-quality-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: eba10d3d-b5c4-447b-8a30-fa07996cb28e
caps.latest.revision: 18
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: e1bc39de73a6e5697c8ab2685b09c78188c36c27
ms.sourcegitcommit: f16003fd1ca28b5e06d5700e730f681720006816
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/11/2018
ms.locfileid: "35310504"
---
# <a name="export-a-domain-to-a-dqs-file"></a>Exportar un dominio a un archivo .dqs

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  En este tema se describe cómo exportar un dominio a un archivo .dqs en [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS). Puede exportar un dominio o una base de conocimiento completa a un archivo de datos. Para obtener información sobre cómo exportar una base de conocimiento, vea [Exportar una base de conocimiento a un archivo .dqs](../data-quality-services/export-a-knowledge-base-to-a-dqs-file.md).  
  
 Exportar un dominio de una base de conocimiento a un archivo de datos .dqs e importarlo a continuación en otra simplifica el proceso de generación del conocimiento, lo que permite ahorrar tiempo y esfuerzo. Le permite compartir con los demás un dominio y su conocimiento.  
  
 Es posible exportar un dominio individual o un dominio compuesto. Un archivo .dqs que contiene un solo dominio incluye todos los datos de dominio incluidas propiedades, valores y reglas de dominio salvo la información de datos de referencia adjunta. Un archivo .dqs que contiene un dominio compuesto incluye todos los datos de este, incluidos todos los datos de los dominios que lo forman, así como las propiedades, relaciones y reglas de dominio compuesto, salvo la información de datos de referencia. Debe volver a adjuntar el dominio o el dominio compuesto a los servicios de datos de referencia adecuados, si es necesario, después de importar el archivo .dqs. Se exportan tanto los datos publicados como los no publicados.  
  
 El archivo de datos .dqs creado por el proceso de exportación se cifra, por lo que no se puede ver el contenido.  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
###  <a name="Prerequisites"></a> Requisitos previos  
 Para exportar un dominio a un archivo de datos .dqs, debe haber creado y seleccionado un dominio individual o un dominio compuesto que contenga varios dominios individuales. No es necesario que disponga de un archivo .dqs; se creará uno automáticamente.  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permissions  
 Debe disponer del rol dqs_kb_editor o dqs_administrator en la base de datos DQS_MAIN para poder exportar un dominio a un archivo de datos .dqs.  
  
##  <a name="Export"></a> Export a domain to a .dqs file  
 La exportación se puede realizar desde cualquier página de administración de dominios. El comando de exportación está disponible tanto en forma de control de la interfaz de usuario como en forma de comando del menú contextual del panel de la lista de dominios.  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Ejecute la aplicación Data Quality Client](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  En la página de inicio de [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , abra una base de conocimiento en la actividad Administración de dominios.  
  
3.  En la página **Administración de dominios** (con cualquier pestaña seleccionada), seleccione un dominio individual o un dominio compuesto en la lista **Dominio** .  
  
4.  Haga clic en el icono **Exportar datos de la base de conocimiento** situado sobre la lista de dominios y, a continuación, haga clic en **Exportar dominio**. O bien, puede hacer clic con el botón secundario en el dominio en la lista **Dominio** , seleccionar **Exportar**y, a continuación, hacer clic en **Exportar dominio**.  
  
5.  En el cuadro de diálogo **Exportar a un archivo de datos**, desplácese a la carpeta en la que quiere guardar el archivo, asígnele un nombre o conserve el predeterminado, mantenga seleccionada la opción **Archivos de datos DQS (\*.dqs)** en la lista **Guardar como tipo** y, luego, haga clic en **Guardar**.  
  
6.  En el cuadro de diálogo **Exportar dominio** , compruebe que la línea de estado de este indica que se ha completado la exportación. Haga clic en **Aceptar**.  
  
##  <a name="FollowUp"></a> Seguimiento: después de exportar un dominio a un archivo .dqs  
 Una vez exportado un dominio a un archivo .dqs, puede importarlo en otra base de conocimiento.  
  
  
