---
title: Carga previa de la memoria caché (SSRS) | Microsoft Docs
description: Aprenda a cargar previamente la caché de un conjunto de datos compartido mediante la creación de un plan de actualización de caché para él en un servidor de informes de Reporting Services.
ms.date: 05/14/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- cache [Reporting Services]
- preloading cache
ms.assetid: 152a1051-8aa5-4c01-bc85-f8be8971b0cd
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 5401d324be7bb59d5be21afa72acebc0a7ab6487
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/09/2020
ms.locfileid: "84548047"
---
# <a name="preload-the-cache"></a>Carga previa de la memoria caché  
  Puede cargar previamente la memoria caché para un conjunto de datos compartido creando un plan de actualización de caché para él.  
  
 Puede cargar previamente la memoria caché para un informe de dos maneras:  
  
1.  Cree un plan de actualización de caché para el informe. Este es el método preferido.  
  
2.  Utilice una suscripción controlada por datos para cargar previamente la memoria caché con instancias de informes con parámetros. Esa era la única manera de cargar previamente la memoria caché en las versiones de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] anteriores a [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]. Para más información, vea [Informes almacenados en caché &#40;SSRS&#41;](../../reporting-services/report-server/caching-reports-ssrs.md).  
  
 Se deben cumplir las siguientes condiciones para poder almacenar en memoria caché un informe o un conjunto de datos compartido:  
  
-   El conjunto de datos compartido o el informe deben tener habilitado el almacenamiento en caché.  
  
-   Los orígenes de datos compartidos para el conjunto de datos compartidos o el informe se deben configurar para utilizar las credenciales almacenadas o para no usar ninguna credencial.  
  
-   Se debe ejecutar el servicio Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="to-preload-the-cache-by-creating-a-cache-refresh-plan"></a>Para cargar previamente la memoria caché creando un plan de actualización de caché  
  
1. Inicie [el portal web de un servidor de informes](../../reporting-services/web-portal-ssrs-native-mode.md "El portal web de un servidor de informes").  
  
2. Seleccione **Examinar** en la pantalla de inicio y navegue por la jerarquía de carpetas para localizar el elemento que desea almacenar en caché.  
  
3. Seleccione los puntos suspensivos que se encuentran en la esquina superior derecha del elemento y luego seleccione **Administrar** en el menú desplegable.  
  
4. Seleccione la pestaña **Almacenamiento en caché** en el menú de vertical de la izquierda.  
  
5. Para activar el almacenamiento en caché para un conjunto de datos, seleccione el botón de radio **Copiar en caché copias de este conjunto de datos y usarlas cuando estén disponibles** . Aparecerá la sección **Expiración de la caché** debajo de él. Seleccione uno de los siguientes botones de radio:

    - **La memoria caché expira después de x minutos** (escriba el número de minutos que desee en x).
    - **La memoria caché expira en una programación.** .  Reporting Services proporciona programaciones compartidas y programaciones específicas de informe para ayudarlo a controlar el procesamiento, el contenido coherente y el rendimiento de la distribución de informes. Para obtener más información, consulte [Create, Modify, and Delete Schedules](../../reporting-services/subscriptions/create-modify-and-delete-schedules.md "Create, Modify, and Delete Schedules"). Tiene varias opciones sobre cómo crear una programación, en este caso para la expiración de caché. Seleccione una de las dos opciones de programación siguientes:  
      - Botón de radio **Programación compartida** y luego seleccione una programación desde el cuadro de texto desplegable **Seleccionar una programación compartida**. Para obtener más información, vea [Schedules](../../reporting-services/subscriptions/schedules.md "Programaciones").  
      - Botón de radio **Programación específica del informe** y luego seleccione el vínculo **Editar programación** si es necesario para mostrar la página *Detalles de programación*.  

         ![Página de detalles de programación de la expiración de caché del portal web para conjuntos de datos](../../reporting-services/report-server/media/preload-the-cache/web-portal-dataset-cache-schedule-details.png "Página detalles de programación de caché de conjunto de datos")

          En esta página puede seleccionar:
         - El tipo de programación:
           - **Hora**: ejecute la programación en horas y minutos específicos así como la hora de inicio.
           - **Día**: seleccione una de las tres opciones siguientes:  
              - **En los siguientes días**: (Dom, Lun, Mar, Mié, Jue, Vie, Sáb).
              - **Todos los días de la semana**
              - **Repetir tras este número de días**: especifique un número.  
           - **Semana**: especifique los dos elementos siguientes:
              - **Repetir tras este número de semanas**: especifique un número.  
              - **En los días**: seleccione los días de la semana para la ejecución.  
           - **Mes**: qué meses, con las siguientes posibilidades de elección:
              - **En la semana del mes**,  
                 - Seleccione (1ª, 2ª, 3ª, 4ª o Última) en el cuadro desplegable.  
                 - **El día de la semana** para la ejecución. Seleccione una o varias de las casillas de verificación (Dom., Lun., Mar., Mié., Jue., Vie., Sáb.).  
                 - **Los días del calendario**: escriba el número real del mes separado por comas, o un intervalo de días separados por un guion, o cualquier combinación de ambos (por ejemplo, 1,3-5).  
           - **Una vez**: una sola aparición.  
         - **Hora de inicio**: hora del día para que se inicie la programación.  
         - **Fechas de inicio y finalización**: especifique la fecha de inicio y, opcionalmente, la fecha de finalización de la programación.
         - Seleccione **Aplicar** para guardar la programación.  
           > [!NOTE]
           > Si el elemento no tiene habilitado el almacenamiento en caché, se solicitará que lo habilite. Para habilitar el almacenamiento en caché, seleccione **Aceptar**.  

         - Seleccione **Crear plan de actualización de caché** para crear o guardar el plan de caché.  
         Se abrirá la página **Planes de actualización de caché**  en la pantalla. Desde aquí, puede:
           - Agregar un nuevo plan de actualización de caché.
           - Crear un nuevo plan de actualización de caché a partir de un plan existente.
           - Actualizar la página de planes de actualización de caché.
           - Eliminar un plan.
           - Buscar un plan por nombre.

         Si aún no se han guardado planes de actualización de caché, la lista estará vacía y la opción "Agregar" será la única disponible. Seleccione **+ Nuevo plan de actualización de caché** para agregar uno nuevo; se mostrará la página **Nuevo plan de actualización de caché** .  
           - Escriba el primer cuadro de texto **Descripción** escriba un nombre para el plan de actualización.  
           - Seleccione uno de los siguientes botones de radio en **Actualizar la memoria caché según la siguiente programación**.  
             - **Programación compartida**: seleccione una programación compartida en el cuadro desplegable adyacente. 
             - **Programación específica del informe**: edite la programación como en el paso 2.2 anterior seleccionando el vínculo **Editar programación** si lo desea para mostrar la página *Detalles de programación*. 
             - Seleccione **Crear plan de actualización de caché**  para guardar el plan si está agregando el plan, o **Aplicar** si está editando el plan.  
      Se le devolverá a la página **Planes de actualización de caché**.
  
## <a name="to-preload-the-cache-with-a-user-specific-report-by-using-a-data-driven-subscription"></a>Para cargar previamente la memoria caché con un informe específico del usuario utilizando una suscripción controlada por datos

1. Inicie [el portal web de un servidor de informes](../../reporting-services/web-portal-ssrs-native-mode.md "El portal web de un servidor de informes").  
2. Seleccione **Examinar** en la pantalla de inicio y navegue por la jerarquía de carpetas para localizar el informe al que desea suscribirse.  
3. Haga clic con el botón derecho en el informe y seleccione **Suscribirse** en el menú desplegable. Se mostrará el página **Nuevas suscripciones**.  
4. Escriba una descripción para la suscripción en el cuadro de texto **Descripción**.  
5. El botón de radio **Tipo de suscripción** muestra dos opciones:  
   - **Suscripción estándar**: para generar y entregar un informe.
   - **Suscripción controlada por datos** : para generar y entregar un informe por cada fila de un conjunto de datos. Esta es la opción que desea seleccionar para cargar previamente la memoria caché.
6. En la sección **Programación**, seleccione uno de los siguientes botones de radio:
   - **Programación compartida**: seleccione una programación compartida en el cuadro desplegable.  
   - **Programación específica del informe**: edite la programación como en el paso 2.2 anterior seleccionando el vínculo **Editar programación** si lo desea para mostrar la página *Detalles de programación*.  
7. La sección **Destino** muestra las siguientes opciones en un cuadro desplegable:
    - **Recurso compartido de archivos de Windows**
    - **Correo electrónico**
    - **Proveedor de entrega NULL**: para esta tarea, seleccione el proveedor de entrega Null.  
8. En la sección **Conjunto de datos**, edite o cree un conjunto de datos para esta suscripción de informe seleccionando el botón **Editar conjunto de datos**.  
9. En la página **Editar conjunto de datos** de la sección **Origen de datos**, elija el origen de datos que contiene los valores de parámetro de informe y las opciones de entrega. Las opciones son:  
   - **Un origen de datos compartido**: seleccione los puntos suspensivos y elija un origen de datos compartido de la carpeta *Origen de datos compartido*.
   - **Un origen de datos personalizado** (lo más probable). Esta es la opción que tendrá que elegir, a menos que usted u otra persona ya haya completado los pasos siguientes para crearlo como un origen de datos compartido.  
     - Especifique el tipo de conexión, la cadena de conexión y las credenciales para obtener acceso al origen de datos que contiene la información sobre los suscriptores. En el siguiente ejemplo, se muestra la cadena de conexión usada para conectarse a una base de datos de SQL Server denominada Subscribers.  
  
   ```T-SQL
   data source=<servername>;initial catalog=Subscribers  
   ```
  
10. En el **Consulta** sección: especifique la consulta que recupera los datos del suscriptor deseado.  Por ejemplo:  
  
    ```T-SQL  
    Select * from RptSubscribers  
    ```
  
    Si lo desea, puede incrementar el período de tiempo de espera en el caso de consultas que tarden bastante tiempo en procesarse.  
  
11. Seleccione **Validar**. Antes de continuar, la consulta debe validarse. Cuando aparezca el mensaje **Validación correcta**, se mostrará una lista de campos de conjunto de datos debajo del botón **Validar**. Seleccione **Aplicar** para crear el origen de datos personalizados.  
  
12. Se le devolverá a la página **Nueva suscripción**.  En la sección **Parámetros del informe**, especifique los valores de parámetro de informe para los parámetros del informe mostrados, si los hay.  

13. Seleccione **Crear suscripción**.  
  
14. Aparece la página **Suscripciones** que muestra la nueva suscripción controlada por datos. Desde esta página puede habilitar la suscripción cuando haya terminado seleccionando la casilla situada a su izquierda y seleccionando el botón **Habilitar**. ![botón habilitar de la página suscripciones](../../reporting-services/report-server/media/preload-the-cache/subscriptions-page-enable-button.png "El botón Habilitar de la página suscripciones")

15. Especifique cuándo se procesa la suscripción. No elija **Cuando los datos del informe se actualizan en el servidor de informes** . Este valor solo es para instantáneas. Si quiere usar una programación existente, seleccione **Según una programación compartida**.  
  
     O bien, para crear una programación personalizada, seleccione **Según una programación creada para esta suscripción** y luego elija **Siguiente**. Configure la programación y seleccione **Finalizar**.  
  
    > [!NOTE]  
    > Para que los suscriptores reciban el informe más reciente, el programa que configure debe ser coherente con la programación de entrega del informe que haya definido para los suscriptores. Para más información, consulte el [portal web de un servidor de informes](../../reporting-services/web-portal-ssrs-native-mode.md  "El portal web de un servidor de informes").  
  
16. Configure las opciones de Ejecución correspondientes al informe de la forma siguiente: En la página del informe, seleccione la pestaña **Propiedades**.  
  
17. En el marco de la izquierda, seleccione la pestaña **Ejecución**.  
  
18. En la página, seleccione **Representar este informe con los datos más recientes**.  
  
19. Elija una de las dos opciones de caché siguientes y configure la expiración como se indica a continuación:  
  
    - Para lograr que la copia en caché expire después de un período de tiempo concreto, seleccione **Almacenar en caché una copia temporal del informe. La copia expirará después de un número determinado de minutos.** Escriba el número de minutos para la expiración del informe.  
  
    - Para lograr que la copia en caché expire según una programación, seleccione **Guardar en caché una copia temporal del informe. La copia del informe debe expirar según la siguiente programación.** Seleccione **Configurar**o seleccione una programación compartida para establecer una programación para la expiración del informe.  
  
20. Seleccione **Aplicar**.
  
## <a name="see-also"></a>Consulte también  

 [Suscripciones controladas por datos](../../reporting-services/subscriptions/data-driven-subscriptions.md)  
 [Crear una suscripción controlada por datos &#40;Tutorial de SSRS&#41;](../../reporting-services/create-a-data-driven-subscription-ssrs-tutorial.md)  
 [Rendimiento, instantáneas, almacenamiento en caché &#40;Reporting Services&#41;](../../reporting-services/report-server/performance-snapshots-caching-reporting-services.md)  
 [Establecimiento de las propiedades del procesamiento de informes](../../reporting-services/report-server/set-report-processing-properties.md)  
 [Informes almacenados en caché &#40;SSRS&#41;](../../reporting-services/report-server/caching-reports-ssrs.md)  
 [Uso de los conjuntos de datos compartidos (portal web)](../../reporting-services/work-with-shared-datasets-web-portal.md)  
  
