---
title: Importar un dominio desde un archivo .dqs | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: fabd88b0-22b3-4543-a993-6d5b202ded80
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: d0e5ffc088918924ae08d4fde2cc7064de1abcbb
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "65484258"
---
# <a name="import-a-domain-from-a-dqs-file"></a>Importar un dominio desde un archivo .dqs
  En este tema se describe cómo importar un dominio desde un archivo .dqs a una base de conocimiento existente de [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS). Los archivos de datos .dqs se crean al exportar un dominio o una base de conocimiento desde la aplicación [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] . El archivo de datos .dqs está cifrado, por lo que no se puede ver.  
  
 El uso de un archivo de datos .dqs para exportar un dominio de una base de conocimiento e importarlo a continuación en otra simplifica el proceso de generación del conocimiento, lo que permite ahorrar tiempo y esfuerzo. Le permite compartir un dominio y su conocimiento con otras personas, ahorrándoles tiempo. Es posible importar tanto un dominio individual como un dominio compuesto (dominio que contiene varios dominios únicos). Un archivo .dqs que contiene un solo dominio incluye todos los datos de dominio incluidas propiedades, valores y datos de reglas de dominio salvo la información de datos de referencia asignada. Un archivo .dqs que contiene un dominio compuesto incluye todos los datos de este, incluidos los de los dominios individuales que lo forman, así como las propiedades, relaciones de valor y reglas de CD del dominio compuesto, salvo los datos de referencia asignados. Se importarán tanto los datos publicados como los no publicados.  
  
 Cuando se importa un dominio, su nombre será el mismo que el del dominio que se exportó originalmente, a menos que ese nombre ya exista, en cuyo caso DQS le agregará la cadena "_1". Lo mismo sucederá si se importa un dominio compuesto que contiene un dominio individual con el mismo nombre que uno ya existente.  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> Requisitos previos  
 Para importar un dominio desde un archivo .dqs, es necesario haber exportado previamente un dominio individual o uno compuesto (que contiene varios dominios individuales) a dicho archivo. El archivo .dqs solo puede incluir un dominio. También debe haber creado y abierto una base de conocimiento en la que importar el dominio.  
  
###  <a name="security"></a><a name="Security"></a> Seguridad  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permisos  
 Debe disponer del rol dqs_kb_editor o dqs_administrator en la base de datos DQS_MAIN para poder importar un dominio desde un archivo de datos .dqs.  
  
##  <a name="import-a-domain-from-a-dqs-file"></a><a name="Import"></a>Importar un dominio desde un archivo. DQS  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][Ejecute la aplicación Data Quality Client](../../2014/data-quality-services/run-the-data-quality-client-application.md).  
  
2.  En la página de inicio de [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , abra una base de conocimiento en la actividad Administración de dominios.  
  
3.  Haga clic en el icono **Importar dominio del archivo de datos** .  
  
4.  En el cuadro de diálogo **Importar de archivo de datos** , desplácese a la carpeta desde la que desea importar el archivo, seleccione este (de tipo Archivo DQS) y, a continuación, haga clic en **Abrir**.  
  
5.  En el cuadro de diálogo **Importar dominio** , haga clic en **Aceptar**.  
  
    > [!NOTE]  
    >  La operación de importación se realizará correctamente únicamente si el archivo .dqs que se está importando solo contiene un dominio individual o un dominio compuesto (que contiene varios dominios individuales).  
  
6.  Compruebe que el dominio que importó aparece en la lista **Dominio** . Si importó un dominio compuesto, compruebe que tanto este como los dominios individuales que lo forman aparecen en la lista **Dominio** .  
  
##  <a name="follow-up-after-importing-a-domain-from-a-dqs-file"></a><a name="FollowUp"></a> Seguimiento: después de importar un dominio desde un archivo .dqs  
 Después de importar un dominio desde un archivo .dqs, puede agregar conocimiento al dominio o utilizarlo en un proyecto de limpieza o de búsqueda de coincidencias, en función de su contenido. Para más información, vea [Realizar la detección de conocimiento](../../2014/data-quality-services/perform-knowledge-discovery.md), [Administrar un dominio](../../2014/data-quality-services/managing-a-domain.md), [Administrar un dominio compuesto](../../2014/data-quality-services/managing-a-composite-domain.md), [Crear una directiva de coincidencia](../../2014/data-quality-services/create-a-matching-policy.md), [Limpieza de datos](../../2014/data-quality-services/data-cleansing.md) o [Coincidencia de datos](../../2014/data-quality-services/data-matching.md).  
  
  
