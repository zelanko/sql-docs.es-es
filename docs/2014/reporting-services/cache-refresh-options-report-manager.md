---
title: Almacenar en caché las opciones de actualización (Administrador de informes) | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 227da40c-6bd2-48ec-aa9c-50ce6c1ca3a6
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 6ae1ee11edd51153585e9a6738bbfbd59af8974f
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66109921"
---
# <a name="cache-refresh-options-report-manager"></a>Opciones de actualización de memoria caché (Administrador de informes)
  Utilice la página Opciones de actualización de caché a fin de crear las programaciones para cargar previamente la memoria caché con copias temporales de datos para un informe o un conjunto de datos compartido. Un plan de actualización incluye una programación y la opción para especificar o invalidar los valores de los parámetros. Para un conjunto de datos compartido, no puede invalidar los valores para los parámetros que estén marcados como de solo lectura. Puede crear y utilizar más de un plan de actualización como parte de la página de opciones de actualización.  
  
 Las asignaciones de roles predeterminadas que permiten agregar, eliminar, cambiar y ver los informes relacionados y los conjuntos de datos compartidos para los planes de actualización de memoria caché son Administrador de contenido, Mis informes y Editor.  
  
> [!NOTE]  
>  Esta característica no está disponible en todas las ediciones de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Para obtener una lista de las características admitidas por las ediciones de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], vea [Features Supported by the Editions of SQL Server 2014](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
## <a name="to-open-the-cache-refresh-plan-properties-page-for-a-report-or-shared-dataset"></a>Para abrir la página de propiedades Plan de actualización de caché para un conjunto de datos compartido o de informe  
  
1.  Abra el Administrador de informes y busque el informe o el conjunto de datos compartido para el que desea configurar las propiedades del plan de actualización de caché.  
  
2.  Mantenga el mouse sobre el informe o el conjunto de datos compartido, y haga clic en la flecha de lista desplegable.  
  
3.  En la lista desplegable, haga clic en **Administrar**. Se abre la página **Propiedades generales** .  
  
4.  Haga clic en la pestaña **Plan de actualización de caché** .  
  
5.  Para crear un nuevo plan de memoria caché, haga clic en **Nuevo plan de actualización de caché**.  
  
    > [!NOTE]  
    >  Debe habilitar e iniciar el servicio del Agente SQL Server para crear un plan de actualización de caché.  
  
6.  Para crear una copia de un plan de caché y, a continuación, personalizarlo, haga clic en **Nuevo a partir de existente**.  
  
## <a name="cache-refresh-options"></a>Opciones de actualización de caché  
 **Eliminar**  
 Elimina todos los planes de actualización seleccionados actualmente.  
  
 **Nuevo a partir de existente**  
 Esta opción se habilita cuando está seleccionado un plan de actualización de caché y solo uno. Esta opción creará un plan de actualización nuevo que se copia a partir del plan original. El plan de actualización de caché se abre rellenado de antemano con detalles del plan que se seleccionara. A continuación puede modificar las opciones del plan de actualización y guardar el plan con otra descripción.  
  
 **Nuevo plan de actualización de caché**  
 Haga clic para crear un nuevo plan de actualización que se usará en las opciones de actualización de caché actuales.  
  
 **Editar**  
 Seleccione esta opción para modificar el plan de actualización actual.  
  
## <a name="cache-refresh-plan-options"></a>Opciones del plan de actualización de caché  
 **Descripción**  
 Especifique una descripción para el plan de actualización de caché.  
  
 **Programación específica del elemento**  
 Seleccione esta opción para crear una programación que se use solo en este informe.  
  
 **Configurar**  
 Haga clic para abrir la página Programación, que se usa para especificar información de frecuencia.  
  
 Para obtener más información, consulte [nueva programación: Editar programación página &#40;el Administrador de informes&#41;](../../2014/reporting-services/new-schedule-edit-schedule-page-report-manager.md).  
  
 **Programación compartida**  
 Seleccione esta opción para seleccionar una programación existente.  
  
 Para obtener más información, consulte [Create, Modify, and Delete Schedules](subscriptions/create-modify-and-delete-schedules.md).  
  
 **@\<** *Parámetro* **>**  
 Especifique una combinación de valores de parámetros. Esta sección solo aparece si el conjunto de datos actual o el informe tienen parámetros.  
  
 Vea [Especificar los parámetros](#Parameters) en la sección siguiente.  
  
 **Usar el valor predeterminado**  
 Seleccione esta opción para usar el valor predeterminado predefinido para este parámetro.  
  
##  <a name="Parameters"></a> Especificación de parámetros  
 Para crear un plan de actualización de caché, cada informe o parámetro de conjunto de datos compartido debe tener un valor. Si el informe o el elemento de conjunto de datos compartido no tienen un valor predeterminado especificado en la definición, debe especificar uno. Si existe un valor predeterminado, no es necesario proporcionarlo aquí. Si proporciona un valor, este invalida el predeterminado.  
  
 Para especificar varias combinaciones de valores de parámetros, cree un plan de actualización de caché independiente para cada combinación.  
  
 Las incorporaciones, cambios y eliminaciones realizados en los parámetros en un informe o conjunto de datos compartido pueden afectar al plan de actualización de caché. Si agrega un parámetro con un valor predeterminado para un informe, quita un parámetro o cambia el tipo de datos o la opción de solo lectura para un parámetro de un conjunto de datos compartido, los cambios surten efecto la próxima vez que se procesa el plan de actualización de caché.  
  
### <a name="shared-dataset-parameters"></a>Parámetros de los conjuntos de datos compartidos  
 En un conjunto de datos compartido, la siguiente información se deriva de la definición del mismo:  
  
-   **Nombre** : especifica el nombre del parámetro de consulta.  
  
-   **Tipo** : especifica el tipo de datos de un parámetro de consulta. Dado que este tipo de datos es desconocido hasta que el proveedor de datos procesa la consulta del conjunto de datos, la validación del tipo de datos no puede producirse hasta que se procesa el conjunto de datos compartido.  
  
-   **Aceptación de valores NULL** : especifica si NULL es un valor válido.  
  
-   **ReadOnly** : especifica si este parámetro se marca como de solo lectura en la definición del conjunto de datos compartido. Los parámetros de solo lectura no aparecen en la lista de parámetros para las opciones de actualización de caché y deben tener un valor predeterminado especificado como parte de la definición del conjunto de datos compartido.  
  
-   **DefaultValues** : los valores predeterminados que se hayan especificado en la definición del conjunto de datos compartido. Los parámetros de consulta pueden tener varios valores. Para invalidar los valores predeterminados, escriba los nuevos valores en las áreas de mensajes del cuadro de texto.  
  
 Si la definición del conjunto de datos compartido especifica la opción **Omitir de la consulta** para un parámetro, no necesita proporcionar un valor predeterminado. Esta marca indica que el parámetro del conjunto de datos no se utiliza en la consulta. Por ejemplo, el parámetro aparece en la definición del conjunto de datos compartido porque es un parámetro de informe que solo se utiliza en el filtro del conjunto de datos.  
  
 Para ver o cambiar las opciones de los parámetros de conjunto de datos, debe modificar la definición del conjunto de datos compartido. Para más información, vea [Administrar conjuntos de datos compartidos](report-data/manage-shared-datasets.md).  
  
### <a name="report-parameters"></a>Parámetros de informe  
 En un informe, cada valor de parámetro debe ser válido para poder crear correctamente un plan de actualización de caché. Debe escribir o seleccionar un valor predeterminado para cada parámetro de informe. El valor que establece invalida el predeterminado que se define para el parámetro de informe en el servidor de informes.  
  
 Los parámetros deben cumplir los requisitos especificados en las propiedades de parámetro en el servidor de informes. Por ejemplo, si la propiedad AllowBlank es false para un parámetro de informe, una cadena vacía no es un valor válido.  
  
 Para ver o cambiar las opciones de los parámetros de informe, debe modificar los parámetros de informe en el informe o independientemente en el servidor de informes. Para obtener más información, consulte [concepto de parámetros de informe &#40;generador de informes y SSRS&#41;](report-design/report-parameters-concepts-report-builder-and-ssrs.md).  
  
## <a name="conditions-that-cause-a-cache-refresh-plan-to-be-inactive"></a>Condiciones que ocasionan que un plan de actualización de caché esté inactivo  
 Las siguientes condiciones pueden hacer que un plan de actualización de caché de un informe o un conjunto de datos compartido se convierta en inactivo.  
  
-   La opción de memoria caché del informe o de memoria caché del conjunto de datos compartido está deshabilitada.  
  
-   Los valores de los parámetros necesarios no están definidos, no son válidos o faltan. Todas las consultas para un informe deben ser válidas antes de que se procese este. En el caso de un informe que tenga subinformes, todas las consultas del conjunto de datos, incluidas los conjuntos de datos del subinforme, se procesan primero. Si no se puede procesar correctamente un conjunto de datos, el informe no se puede ejecutar.  
  
## <a name="conditions-that-cause-a-cache-refresh-plan-to-be-reactivated"></a>Condiciones que ocasionan que se reactive un plan de actualización de caché  
 Una vez que un plan está inactivo, elija una de las opciones siguientes para activar la evaluación de otro plan de actualización de caché:  
  
-   Cambie una opción para el plan.  
  
-   Habilite el almacenamiento en caché para un conjunto de datos compartido o un informe que esté asociado al plan de actualización.  
  
-   Active o desactive la opción de solo lectura para un parámetro de consulta del conjunto de datos asociado al plan de actualización y, a continuación, guarde la nueva definición en el servidor de informes.  
  
## <a name="see-also"></a>Vea también  
 [Tareas de nivel de elemento](security/tasks-and-permissions-item-level-tasks.md)   
 [Administrador de informes &#40;Modo nativo de SSRS&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [El Administrador de informes (Ayuda F1)](../../2014/reporting-services/report-manager-f1-help.md)   
 [Informes almacenados en caché &#40;SSRS&#41;](report-server/caching-reports-ssrs.md)   
 [Administración de conjuntos de datos compartidos](report-data/manage-shared-datasets.md)  
  
  
