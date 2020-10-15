---
title: Configuración de las propiedades de ejecución de un informe - Administrador de informes | Microsoft Docs
description: Obtenga información sobre cómo establecer opciones de procesamiento de informes para especificar cuándo se deben recuperar los datos de informe para evitar la sobrecarga de recuperar los mismos datos cada vez que se solicita un informe.
ms.date: 06/26/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reports
ms.topic: conceptual
helpviewer_keywords:
- report execution properties [Reporting Services]
- reports [Reporting Services], properties
- reports [Reporting Services], execution options
ms.assetid: 73cc8dcc-ef80-40d7-9739-d33bba0eb28a
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 13b74b5437eb9df1cd51425929ffb70770595a69
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/13/2020
ms.locfileid: "91988393"
---
# <a name="configure-execution-properties-for-a-report"></a>Configurar las propiedades de ejecución para un informe
  Puede establecer las opciones de procesamiento de informes para especificar cuándo se recuperan los datos para un informe. Resulta útil programar el procesamiento de datos para un informe si el origen de datos externo se actualiza en momentos concretos (por ejemplo, un almacenamiento de datos que se actualiza diariamente o semanalmente) y desea evitar la sobrecarga de recuperar los mismos datos cada vez que se solicita un informe. La programación del procesamiento de datos también resulta útil si desea controlar la carga del procesamiento en el servidor de bases de datos externo o si desea proporcionar resultados coherentes para varios usuarios que deben trabajar con conjuntos idénticos de datos. Si los datos no son estables, un informe a petición puede producir resultados diferentes en pocos minutos. Por el contrario, una instantánea de informe permite hacer comparaciones válidas con otros informes o herramientas de análisis que tengan los datos existentes en el mismo instante.  
  
 Una instantánea de informe es un informe que contiene instrucciones de diseño y resultados de consultas que se recuperaron en un momento concreto. A diferencia de los informes a petición, que obtienen resultados de consulta actualizados cuando se seleccionan, las instantáneas de informe se procesan según una programación y luego se guardan en un servidor de informes. Al seleccionar una instantánea de informe para su visualización, el servidor de informes recupera el informe almacenado en la base de datos del servidor de informes y muestra los datos y el diseño actualizados para el informe en el momento en que se creó la instantánea.  
  
 Las instantáneas de informe no se guardan con un formato de representación concreto. En su lugar, las instantáneas de informe se representan en un formato de visualización final (como HTML) solo cuando un usuario o una aplicación lo solicita. La representación aplazada hace que las instantáneas sean portátiles. El informe se puede representar con el formato correcto para el dispositivo o explorador web que lo solicita.  

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
  
## <a name="to-configure-report-processing-options"></a>Para configurar las opciones de procesamiento de informe  
  
1.  Inicie el [Administrador de informes &#40;Modo nativo de SSRS&#41;](../web-portal-ssrs-native-mode.md).  
  
2.  Navegue hasta el informe para el que desea establecer las opciones de procesamiento y ábralo.  
  
 Mantenga el mouse sobre el informe y haga clic en la flecha de lista desplegable.  
  
1.  En el menú desplegable, haga clic en **Administrar** y, después, seleccione la pestaña **Opciones de procesamiento** .  
  
2.  Haga clic en **Representar este informe a partir de una instantánea de ejecución y seleccione una de las opciones siguientes:**  
  
    -   Si quiere crear una instantánea, seleccione **Utilizar la siguiente programación para crear instantáneas de ejecución de informes**y, después, defina una programación específica del informe o seleccione una de la lista **Programación compartida** .  
  
    -   Si desea crear una instantánea inmediatamente, seleccione **Crea una instantánea de informe cuando hace clic en el botón Aplicar de esta página**.  
  
3.  Haga clic en **Aplicar**.  
  
## <a name="see-also"></a>Consulte también  
 [Establecer las propiedades del procesamiento de informes](../../reporting-services/report-server/set-report-processing-properties.md)   
 [Contenido &#40;página del Administrador de informes&#41;](/previous-versions/sql/sql-server-2016/ms186470(v=sql.130))   
 [Administración de contenido del servidor de informes &#40;Modo nativo de SSRS&#41;](../../reporting-services/report-server/report-server-content-management-ssrs-native-mode.md)   
 [Página de propiedades Opciones de procesamiento &#40;Administrador de informes&#41;](/previous-versions/sql/sql-server-2016/ms178821(v=sql.130))  
  
::: moniker-end

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
  
## <a name="to-configure-report-execution-properties"></a>Para configurar las propiedades de la ejecución de informes  
  
Desde [el portal web de un servidor de informes (modo nativo de SSRS)](../../reporting-services/web-portal-ssrs-native-mode.md):  
  
1. Navegue al informe para el que desea configurar las propiedades de ejecución.  
  
2. Haga clic con el botón derecho en el informe y seleccione **Administrar** en el menú desplegable.

3. Seleccione la pestaña **Instantáneas del historial** para mostrar la página **Instantáneas del historial**.  
  
4. Seleccione el botón **Programaciones y configuración** y active la opción **Crear instantáneas del historial en un programa** si aún no está activada.
  
5. Seleccione una **Programación compartida** o **Programación específica del informe** según estime oportuno.  
  
6. En la sección **Avanzado**, seleccione la directiva de **Retención** que desee para las instantáneas del historial.  
  
7. Seleccione **Aplicar**.  
  
   >[!NOTE]
   >Si desea crear una instantánea inmediatamente, seleccione el botón **Nueva instantánea del historial** en lugar del botón **Programaciones y configuración** y se creará una instantánea de informe inmediatamente.  
  
## <a name="see-also"></a>Consulte también  
 [Establecer las propiedades del procesamiento de informes](../../reporting-services/report-server/set-report-processing-properties.md)   
 [Administración de contenido del servidor de informes (modo nativo de SSRS)](../../reporting-services/report-server/report-server-content-management-ssrs-native-mode.md)   
 [Establecimiento de las propiedades del procesamiento de informes](../../reporting-services/report-server/set-report-processing-properties.md)   

::: moniker-end