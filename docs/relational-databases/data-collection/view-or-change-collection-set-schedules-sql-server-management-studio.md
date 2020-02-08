---
title: Visualización o cambio de programaciones de conjuntos de recopilación
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql13.swb.dc.collectionsetprop.uploads.f1
- sql13.swb.dc.collectionsetprop.description.f1
- sql13.swb.dc.collectionsetprop.general.f1
helpviewer_keywords:
- collection sets [SQL Server], changing schedules
- schedules [SQL Server], changing collection set
- collection sets [SQL Server], viewing schedules
- schedules [SQL Server], viewing collection set
ms.assetid: 26336c98-78c5-414f-8d6a-574fc3af60c4
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: e38b03a9e903666593567bf34eaa50c578de6825
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "74055332"
---
# <a name="view-or-change-collection-set-schedules-sql-server-management-studio"></a>Ver o cambiar las programaciones del conjunto de recopilación (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Puede ver o cambiar las programaciones del conjunto de recopilación mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 El modo de recopilación, con almacenamiento en caché o sin almacenamiento en caché, determina cómo se puede hacer cambios en una programación. El modo de almacenamiento en caché utiliza programaciones independientes para la recopilación y para la carga. El modo sin almacenamiento en caché utiliza la misma programación para la recopilación y para la carga. El tipo de modo de recopilación para cada uno de los conjuntos de recopilación de datos del sistema es el siguiente:  
  
-   **Uso de disco** : usa el modo de recopilación de datos no almacenados en memoria caché.  
  
-   **Estadísticas de consultas** : utiliza el modo de recopilación de datos almacenados en caché.  
  
-   **Actividad del servidor** : utiliza el modo de recopilación de datos almacenados en caché.  
  
### <a name="to-view-collection-set-schedules"></a>Para ver las programaciones del conjunto de recopilación  
  
1.  En el Explorador de objetos, expanda el nodo **Administración** , expanda **Recopilación de datos**y, después, **Conjuntos de recopilación de datos del sistema**.  
  
2.  Haga clic con el botón derecho en un nombre de conjunto de recopilación y haga clic en **Propiedades** para abrir el cuadro de diálogo [Propiedades del conjunto de recopilación de datos](#CollectionSet) .  
  
### <a name="to-change-the-schedules-for-a-cached-mode-collection-set"></a>Para cambiar las programaciones de un conjunto de recopilación en modo de datos almacenados en caché  
  
1.  En el Explorador de objetos, expanda el nodo **Administración** , expanda **Recopilación de datos**y, después, **Conjuntos de recopilación de datos del sistema**.  
  
2.  Haga clic con el botón derecho en un conjunto de recopilación que use el modo de almacenamiento en memoria caché, como **Estadísticas de consultas**y haga clic en **Propiedades** para abrir el cuadro de diálogo [Propiedades del conjunto de recopilación de datos](#CollectionSet) .  
  
3.  Puede cambiar la frecuencia de recopilación en la página **General** . Para ello, siga estos pasos.  
  
    1.  En el panel de detalles, haga doble clic en el número que se muestra para la columna **Frecuencia de recopilación (s)** en la tabla **Elementos de recopilación** .  
  
    2.  Para aumentar o disminuir la frecuencia de recopilación, escriba un número menor o mayor, y presione ENTRAR para almacenar el nuevo valor.  
  
4.  Para cambiar la programación de carga existente del conjunto de recopilación, siga estos pasos:  
  
    1.  Haga clic en la página **Cargas** .  
  
    2.  En el panel de detalles, haga clic en **Elegir**.  
  
         Se abre el cuadro de diálogo **Elegir programación para trabajo** . Las programaciones disponibles aparecen en forma de tabla.  
  
    3.  Haga clic en la fila con la programación que desee. Por ejemplo, para cambiar la programación a cada 5 minutos, haga clic en la fila donde el nombre de programación sea **CollectorSchedule_Every_5min**.  
  
        > [!NOTE]  
        >  Puede ver y modificar las propiedades de la programación seleccionada haciendo clic en **Propiedades** para abrir el cuadro de diálogo **Propiedades de programación del trabajo** correspondiente a la programación. Puede usar este cuadro de diálogo para cambiar información de la programación, como la frecuencia.  
        >   
        >  Como alternativa a modificar una programación existente, puede hacer clic en **Nueva** , en la página **Cargas** , para crear una programación de carga nueva. De este modo se abre el cuadro de diálogo **Nueva programación de trabajo** , que puede utilizar para crear una programación personalizada.  
  
    4.  Cuando haya terminado de configurar la programación, haga clic en **Aceptar**.  
  
         Los cambios que haga se muestran en la página **Cargas** .  
  
5.  Haga clic en **Aceptar** para guardar los cambios de la frecuencia de recopilación y la programación de carga y para cerrar el cuadro de diálogo **Propiedades del conjunto de recopilación de datos** .  
  
### <a name="to-change-the-schedule-for-a-non-cached-mode-collection-set"></a>Para cambiar la programación de un conjunto de recopilación en modo de datos no almacenados en caché  
  
1.  En el Explorador de objetos, expanda el nodo **Administración** , expanda **Recopilación de datos**y, después, **Conjuntos de recopilación de datos del sistema**.  
  
2.  Haga clic con el botón derecho en un conjunto de recopilación que use el modo sin almacenamiento en memoria caché, como **Uso de disco**, y haga clic en **Propiedades** para abrir el cuadro de diálogo [Propiedades del conjunto de recopilación de datos](#CollectionSet) .  
  
     El cuadro de diálogo **Propiedades del conjunto de recopilación de datos** muestra una vista paginada de las propiedades del conjunto de recopilación.  
  
3.  Para cambiar la programación de un conjunto de recopilación, haga clic en **Elegir**.  
  
     Se abre el cuadro de diálogo **Elegir programación para trabajo** . Las programaciones disponibles se muestran en forma de tabla.  
  
4.  Haga clic en la fila con la programación que desee. Por ejemplo, para cambiar la programación a cada 5 minutos, haga clic en la fila donde el nombre de programación sea **CollectorSchedule_Every_5min**.  
  
    > [!NOTE]  
    >  Puede ver y modificar las propiedades de la programación seleccionada haciendo clic en **Propiedades** para abrir el cuadro de diálogo **Propiedades de programación del trabajo** correspondiente a la programación. Puede usar este cuadro de diálogo para cambiar información de la programación, como la frecuencia.  
    >   
    >  Como alternativa a modificar una programación existente, puede hacer clic en **Nueva** , en la página **General** , para crear una recopilación y una programación de carga nuevas. De este modo se abre el cuadro de diálogo **Nueva programación de trabajo** .  
  
5.  Cuando haya terminado de configurar la programación, haga clic en **Aceptar**.  
  
6.  Haga clic en **Aceptar** para guardar los cambios y cerrar el cuadro de diálogo **Propiedades del conjunto de recopilación de datos** .  
  
####  <a name="CollectionSet"></a> Cuadro de diálogo Propiedades del conjunto de recopilación de datos  
 **Página General**  
  
 Utilice esta página para configurar la recopilación y carga de datos, las programaciones y los períodos de retención de datos en el almacén de administración de datos. Esta página también proporciona información sobre los conjuntos de recopilación, como los tipos de recopilador y las frecuencias de recopilación, así como sobre los parámetros de entrada que se utilizan para un conjunto de recopilación.  
  
 **Nombre**  
 Muestra el nombre del conjunto de recopilación al que hace referencia esta página.  
  
 **Recopilación y carga de datos**  
 Especifica cómo se recopilan y cargan los datos en el almacén de administración de datos. Elija una de las opciones siguientes.  
  
|||  
|-|-|  
|**Sin caché. Recopilación y carga de datos en la misma programación.**|Si la selecciona, especifique una de las siguientes opciones:<br /><br /> **Programación**. Los datos se recopilan y se cargan de acuerdo con una programación. Haga clic en **Seleccionar** para seleccionar entre una lista predefinida de programaciones o en **Nueva** para crear una nueva programación.<br /><br /> **A petición**. Los datos se recopilan y se cargan a petición.|  
|**En caché. Recopilar y almacenar en caché los datos en un conjunto de frecuencias de recopilación. Cargar los datos en caché según una programación independiente.**|Recopilar y almacenar en caché los datos para una frecuencia de recopilación especificada. Cargar los datos recopilados según una programación independiente.|  
  
 **Elementos de recopilación**  
 Muestra los elementos de recopilación del conjunto de recopilación. Se proporciona la información siguiente para cada elemento de recopilación:  
  
-   **Nombre**  
  
-   **Tipo de recopilador**  
  
-   **Frecuencia de recopilación** (s). Este campo se puede modificar si **Recopilación y carga de datos** se configura como almacenado en caché. Haga doble clic en esta celda para establecer la frecuencia de recopilación.  
  
 **Parámetros de entrada**  
 Muestra los parámetros de entrada utilizados para el conjunto de recopilación.  
  
 **Ejecutar como**  
 Especifica la cuenta utilizada para ejecutar el conjunto de recopilación. De forma predeterminada, ésta es la cuenta del servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Si se definen cuentas de proxy, esta lista incluye los nombres de las cuentas de proxy disponibles.  
  
 **Establecer cuánto tiempo se retendrán los datos recopilados en el almacén de administración de datos.**  
 Especifica cuánto tiempo se retienen los datos recopilados. Elija una de las opciones siguientes.  
  
|||  
|-|-|  
|**Retener datos para**|Esta opción está seleccionada de forma predeterminada y el período de retención predeterminado es de 14 días.|  
|**Retener datos indefinidamente**|No hay ningún límite en la cantidad de tiempo que se retienen los datos.|  
  
 **Página Cargas**  
  
 Utilice esta página para configurar la programación de carga para los datos recogidos por este conjunto de recopilación.  
  
> [!NOTE]  
>  Esta pestaña solo está habilitada si se configura la opción **En caché** para **Recopilación y carga de datos**.  
  
 **Server**  
 Muestra el nombre del servidor que hospeda el almacén de administración de datos. Para obtener más información, vea [Configurar el almacén de administración de datos &#40;SQL Server Management Studio&#41;](../../relational-databases/data-collection/configure-the-management-data-warehouse-sql-server-management-studio.md).  
  
 **almacén de administración de datos**  
 Muestra el nombre del almacén de administración de datos. Para obtener más información, vea [Configurar el almacén de administración de datos &#40;SQL Server Management Studio&#41;](../../relational-databases/data-collection/configure-the-management-data-warehouse-sql-server-management-studio.md).  
  
 **Última carga**  
 Muestra la información de fecha y hora para la última carga del conjunto de recopilación.  
  
 **Programación de carga**  
 Especifica la programación de carga para el conjunto de recopilación. Si está habilitada, haga clic en **Seleccionar** para seleccionar entre una lista predefinida de programaciones o en **Nueva** para crear una nueva programación.  
  
 **Página Descripción**  
  
 Utilice esta página para ver una descripción del conjunto de recopilación al que hace referencia esta página de propiedades.  
  
## <a name="see-also"></a>Consulte también  
 [Administrar la recopilación de datos](../../relational-databases/data-collection/manage-data-collection.md)   
 [Recopilación de datos](../../relational-databases/data-collection/data-collection.md)  
  
  
