---
title: Ayuda F1 del Asistente para la administración de particiones | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
f1_keywords:
- sql13.swb.managepartition.createjob.f1
- sql13.swb.managepartition.progress.f1
- sql13.swb.managepartition.getstart.f1
- sql13.swb.managepartition.selectswitchtables.f1
- sql13.swb.managepartition.stagingtable.f1
- sql13.swb.managepartition.switchin.f1
- sql13.swb.managepartition.switchout.f1
- sql13.swb.managepartition.partitionaction.f1
- sql13.swb.managepartition.summary.f1
- sql13.swb.managepartition.selectoutput.f1
helpviewer_keywords:
- wizards [SQL Server Management Studio] See Manage Partition Wizard
ms.assetid: e2478d26-dea4-428d-98c5-aad2d2a30da8
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: dc76237530ba47a513aba164260061ec6b20e7c3
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/09/2019
ms.locfileid: "68892408"
---
# <a name="manage-partition-wizard-f1-help"></a>Ayuda F1 del Asistente para la administración de particiones
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Utilice el **Asistente para la administración de particiones** con el fin de administrar y modificar las tablas con particiones existentes a través de la activación de particiones o de la implementación de un escenario de ventanas deslizantes. Este asistente puede facilitar la administración de las particiones y simplificar la migración normal de los datos en las tablas.  
  
### <a name="to-start-the-manage-partition-wizard"></a>Para iniciar el Asistente para la administración de particiones  
  
-   En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], seleccione la base de datos, haga clic con el botón derecho en la tabla en la que quiera crear las particiones, seleccione **Almacenamiento**y haga clic en **Administrar partición**.  
  
     **Note** Si la opción **Administrar partición** no está disponible, puede que haya seleccionado una tabla que no contenga particiones. Haga clic en **Crear partición** en el submenú **Almacenamiento** y utilice el **Asistente para la creación de particiones** con el fin de crear las particiones en la tabla.  
  
 Para obtener información general sobre particiones e índices, vea [Partitioned Tables and Indexes](../../relational-databases/partitions/partitioned-tables-and-indexes.md).  
  
 En esta sección se proporciona la información necesaria para administrar, modificar e implementar particiones utilizando el **Asistente para la administración de particiones**.  
  
##  <a name="Top"></a> En esta sección  
 En las secciones siguientes se proporciona ayuda de las páginas del **Asistente para la administración de particiones**.  
  
 [Asistente para la administración de particiones (página Seleccionar acción de partición)](#SelectPartitionAction)  
  
 [Asistente para administrar particiones (página Activar partición)](#SwitchIn)  
  
 [Asistente para administrar particiones (página Desactivar partición)](#SwitchOut)  
  
 [Asistente para la administración de particiones (página Seleccionar las opciones de tabla de ensayo)](#StagingTableOptions)  
  
 [Asistente para la administración de particiones (página Seleccionar opción de salida)](#OutputOption)  
  
 [Asistente para la administración de particiones (página Nueva programación de trabajo)](#NewJob)  
  
 [Asistente para la administración de particiones (página Resumen)](#Summary)  
  
 [Asistente para la administración de particiones (página Progreso)](#Progress)  
  
##  <a name="SelectPartitionAction"></a> Página Seleccionar acción de partición  
 Utilice la página **Seleccionar acción de partición** para elegir la acción que desee realizar en la partición.  
  
### <a name="create-a-staging-table"></a>Crear una tabla de ensayo  
 La activación y desactivación de particiones es una tarea común de las particiones si tiene una tabla con particiones para la migración de datos de forma regular; por ejemplo, si tiene una tabla con particiones que almacena datos trimestrales actuales y le debe pasar datos nuevos y archivar datos antiguos al final de cada trimestre.  
  
 El asistente diseña la tabla de ensayo con la misma estructura de tablas, columnas y columnas de partición, e índices, y almacena la tabla nueva en el grupo de archivos en los que se encuentra la partición de origen.  
  
 Para crear una tabla de ensayo en la que activar o desactivar las particiones de los datos, seleccione **Crear una tabla de ensayo para la modificación de particiones**.  
  
### <a name="sliding-window-scenario"></a>Escenario de ventana deslizante  
 Para administrar las particiones en un escenario de ventana deslizante, seleccione **Administrar datos particionados en un escenario de ventana deslizante**.  
  
## <a name="uielement-list"></a>Lista de UIElement  
 **Crear una tabla de ensayo para la modificación de particiones**  
 Crea una tabla de ensayo para los datos cuya partición está activando o desactivando en la tabla con particiones existente.  
  
 **Desactivar partición**  
 Proporciona opciones al quitar una partición de la tabla.  
  
 **Activar partición**  
 Proporciona opciones al agregar una partición a la tabla.  
  
 **Administrar datos particionados en un escenario de ventana deslizante**  
 Anexa una partición vacía a la tabla existente que se puede utilizar para activar la partición de los datos. Actualmente, el asistente permite activar la última partición y desactivar la primera.  
  
 ![Icono de flecha usado con el vínculo Volver al principio](https://docs.microsoft.com/analysis-services/analysis-services/instances/media/uparrow16x16.gif "Icono de flecha usado con el vínculo Volver al principio")[En esta sección](#Top)  
  
##  <a name="SwitchIn"></a> Página Seleccionar las opciones de activación de la partición  
 Use la página **Seleccionar las opciones de activación de la partición** para seleccionar la tabla de ensayo que quiera activar en la tabla con particiones.  
  
## <a name="uielement-list"></a>Lista de UIElement  
 **Mostrar todas las particiones**  
 Seleccione esta opción para mostrar todas las particiones, incluidas las particiones existentes actualmente en la tabla con particiones.  
  
 **Cuadrícula Partición**  
 Muestra el nombre de la partición, el **Límite izquierdo**, el **Límite derecho**, el **Grupo de archivos**y el **Recuento de filas** de las particiones seleccionadas.  
  
 **Tabla de activación**  
 Seleccione la tabla de ensayo que contiene la partición que desea agregar a la tabla con particiones. Debe crear esta tabla de almacenamiento provisional antes de activar las particiones con el **Asistente para la administración de particiones**.  
  
 ![Icono de flecha usado con el vínculo Volver al principio](https://docs.microsoft.com/analysis-services/analysis-services/instances/media/uparrow16x16.gif "Icono de flecha usado con el vínculo Volver al principio")[En esta sección](#Top)  
  
##  <a name="SwitchOut"></a> Página Seleccionar las opciones de desactivación de la partición  
 Use la página **Seleccionar las opciones de desactivación de la partición** para seleccionar la partición y la tabla de ensayo donde se almacenarán los datos particionados que está desactivando en la tabla con particiones.  
  
## <a name="uielement-list"></a>Lista de UIElement  
 **Cuadrícula Partición**  
 Muestra el nombre de la partición, el **Límite izquierdo**, el **Límite derecho**, el **Grupo de archivos**y el **Recuento de filas** de las particiones seleccionadas.  
  
 **Tabla de desactivación**  
 Seleccione una tabla nueva o una tabla existente en la que desea desactivar los datos.  
  
 **Nueva**  
 Escriba un nombre nuevo para la tabla de ensayo que desea utilizar para desactivar la partición de la tabla de origen actual.  
  
 **Existente**  
 Seleccione el nombre de la tabla de ensayo existente que desee utilizar para desactivar la partición de la tabla de origen actual. Si la tabla existente contiene datos, estos se sobrescribirán con los datos cuya partición esté desactivando.  
  
 ![Icono de flecha usado con el vínculo Volver al principio](https://docs.microsoft.com/analysis-services/analysis-services/instances/media/uparrow16x16.gif "Icono de flecha usado con el vínculo Volver al principio")[En esta sección](#Top)  
  
##  <a name="StagingTableOptions"></a> Página Seleccionar las opciones de tabla de ensayo  
 Utilice la página **Seleccionar las opciones de tabla de ensayo** para crear la tabla de ensayo que desea utilizar para modificar los datos con particiones.  
  
 Las tablas de ensayo deben residir en el mismo grupo de archivos que la partición seleccionada en que se encuentra la tabla de origen. La tabla de ensayo debe reflejar el diseño tanto de la tabla de origen como de la tabla de destino.  
  
 También puede crear en la tabla de ensayo los mismos índices que existan en la partición de origen. La tabla de ensayo contiene automáticamente una restricción basada en los elementos de la partición de origen. Esta restricción se suele generar a partir del valor de límite de la partición de origen.  
  
## <a name="uielement-list"></a>Lista de UIElement  
 **Nombre de tabla de ensayo**  
 Cree un nombre para la tabla de ensayo o acepte el predeterminado que se muestra en el cuadro de edición.  
  
 **Cambiar de partición**  
 Seleccione la partición de origen que desea desactivar de la tabla actual.  
  
 **Nuevo valor de límite**  
 Seleccione o escriba el valor de límite que desea para la partición en la tabla de ensayo.  
  
 **Grupo de archivos**  
 Seleccione un grupo de archivos para la nueva tabla.  
  
 ![Icono de flecha usado con el vínculo Volver al principio](https://docs.microsoft.com/analysis-services/analysis-services/instances/media/uparrow16x16.gif "Icono de flecha usado con el vínculo Volver al principio")[En esta sección](#Top)  
  
##  <a name="OutputOption"></a> Página Seleccionar la opción de salida  
 Utilice la página **Seleccionar la opción de salida** para especificar cómo desea completar las modificaciones de las particiones.  
  
### <a name="create-script"></a>Crear script  
 Cuando el asistente finaliza, crea un script en el Editor de consultas para modificar las particiones en la tabla. Seleccione **Crear script** si desea revisar el script y, a continuación, ejecutarlo manualmente.  
  
 **Generar script en archivo**  
 Permite generar el script en un archivo .sql. Especifique **Unicode** o **Texto ANSI**. Para especificar el nombre y la ubicación del archivo, haga clic en **Examinar**.  
  
 **Generar script en Portapapeles**  
 Guarda el script en el Portapapeles.  
  
 **Generar script en la ventana Nueva consulta**  
 Genera el script en una ventana del Editor de consultas. Si no hay ninguna ventana del editor abierta, se abre una ventana nueva como destino del script.  
  
### <a name="run-immediately"></a>Ejecutar inmediatamente  
 **Run immediately**  
 Hace que el asistente finalice las modificaciones en las particiones cuando se hace clic en **Siguiente** o **Finalizar**.  
  
### <a name="schedule"></a>Programación  
 Seleccione esta opción para modificar las particiones de la tabla en una fecha y hora programadas.  
  
 **Cambiar programación**  
 Abre el cuadro de diálogo **Nueva programación de trabajo** , donde puede seleccionar, cambiar o ver las propiedades del trabajo programado.  
  
 ![Icono de flecha usado con el vínculo Volver al principio](https://docs.microsoft.com/analysis-services/analysis-services/instances/media/uparrow16x16.gif "Icono de flecha usado con el vínculo Volver al principio")[En esta sección](#Top)  
  
##  <a name="NewJob"></a> Página Nueva programación del trabajo  
 Utilice la página **Nueva programación del trabajo** para ver y cambiar las propiedades de la programación.  
  
### <a name="options"></a>Opciones  
 Seleccionar el tipo de programación que desea para el trabajo del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **Nombre**  
 Escriba un nuevo nombre de la programación.  
  
 **Trabajos en programación**  
 Vea los trabajos existentes que utilizan la programación.  
  
 **Tipo de programación**  
 Seleccione el tipo de programación.  
  
 **Enabled**  
 Habilite o deshabilite la programación.  
  
### <a name="recurring-schedule-types-options"></a>Opciones de tipos de programación periódica  
 Seleccione la frecuencia del trabajo programado.  
  
 **Sucede**  
 Seleccione el intervalo con el que se repite la programación.  
  
 **Se repite cada**  
 Seleccione el número de días o semanas entre las repeticiones de la programación. Esta opción no está disponible para las programaciones de periodicidad mensual.  
  
 **Lunes**  
 Configure el trabajo para que tenga lugar el lunes. Solo está disponible para las programaciones de periodicidad semanal.  
  
 **Martes**  
 Configure el trabajo para que tenga lugar el martes. Solo está disponible para las programaciones de periodicidad semanal.  
  
 **Miércoles**  
 Configure el trabajo para que tenga lugar el miércoles. Solo está disponible para las programaciones de periodicidad semanal.  
  
 **Jueves**  
 Configure el trabajo para que tenga lugar el jueves. Solo está disponible para las programaciones de periodicidad semanal.  
  
 **Viernes**  
 Configure el trabajo para que tenga lugar el viernes. Solo está disponible para las programaciones de periodicidad semanal.  
  
 **Sábado**  
 Configure el trabajo para que tenga lugar el sábado. Solo está disponible para las programaciones de periodicidad semanal.  
  
 **Domingo**  
 Configure el trabajo para que tenga lugar el domingo. Solo está disponible para las programaciones de periodicidad semanal.  
  
 **Day**  
 Seleccione el día del mes en el que se ejecutará la programación. Solo está disponible para las programaciones mensuales.  
  
 **de cada**  
 Seleccione el número de meses entre las repeticiones de la programación. Solo está disponible para las programaciones mensuales.  
  
 **El**  
 Especifique una programación para un día determinado de la semana, en un semana determinada del mes. Solo está disponible para las programaciones mensuales.  
  
 **Sucede una vez a las**  
 Establezca la hora para que el trabajo se produzca diariamente.  
  
 **Sucede cada**  
 Establece el número de horas o minutos entre repeticiones.  
  
 **Fecha de inicio**  
 Establece la fecha en que comienza a ser efectiva esta programación.  
  
 **Fecha de finalización**  
 Establece la fecha en que deja de ser efectiva la programación.  
  
 **Sin fecha de finalización**  
 Especifica que la programación será efectiva indefinidamente.  
  
### <a name="one-time-schedule-types-options"></a>Opciones de tipos de programación de una sola vez  
 Si programa un trabajo para ejecutarse una vez, debe seleccionar una fecha y hora futuras.  
  
 **Date**  
 Seleccione la fecha de ejecución del trabajo.  
  
 **Time**  
 Seleccione la hora de ejecución del trabajo.  
  
 ![Icono de flecha usado con el vínculo Volver al principio](https://docs.microsoft.com/analysis-services/analysis-services/instances/media/uparrow16x16.gif "Icono de flecha usado con el vínculo Volver al principio")[En esta sección](#Top)  
  
##  <a name="Summary"></a> Página Resumen  
 Utilice la página **Resumen** para revisar las opciones que ha seleccionado en las páginas anteriores.  
  
## <a name="uielement-list"></a>Lista de UIElement  
 **Revisar opciones seleccionadas**  
 Muestra las selecciones que ha realizado en cada página del asistente. Haga clic en un nodo para expandir y ver sus opciones seleccionadas previamente.  
  
 ![Icono de flecha usado con el vínculo Volver al principio](https://docs.microsoft.com/analysis-services/analysis-services/instances/media/uparrow16x16.gif "Icono de flecha usado con el vínculo Volver al principio")[En esta sección](#Top)  
  
##  <a name="Progress"></a> Página Progreso  
 Utilice la página **Progreso** para supervisar la información de estado sobre las acciones del **Asistente para la administración de particiones**. Según las opciones que se seleccionen en el asistente, la página **Progreso** puede contener una o varias acciones. El cuadro superior muestra el estado general del asistente y el número de mensajes de estado, error y advertencia que ha recibido.  
  
### <a name="options"></a>Opciones  
 **Detalles**  
 Proporciona la acción, el estado y los mensajes devueltos por la acción llevada a cabo por el asistente.  
  
 **Acción**  
 Especifica el tipo y el nombre de cada acción.  
  
 **Estado**  
 Indica si la acción del asistente como conjunto ha devuelto el valor **Correcto** o **Error**.  
  
 **de mensaje**  
 Proporciona los mensajes de error o de advertencia devueltos por el proceso.  
  
 **Detener**  
 Detiene la acción llevada a cabo por el asistente.  
  
 **Informe**  
 Crea un informe que contiene los resultados del **Asistente para la administración de particiones**. Las opciones son:  
  
-   **Ver informe**  
  
-   **Guardar informe en archivo**  
  
-   **Copiar informe al Portapapeles**  
  
-   **Enviar informe como correo electrónico**  
  
 **Ver informe**  
 Abre el cuadro de diálogo **Ver informe** . Este cuadro de diálogo contiene un informe de texto con el progreso del **Asistente para la administración de particiones**.  
  
 **Cerrar**  
 Cierra el asistente.  
  
 ![Icono de flecha usado con el vínculo Volver al principio](https://docs.microsoft.com/analysis-services/analysis-services/instances/media/uparrow16x16.gif "Icono de flecha usado con el vínculo Volver al principio")[En esta sección](#Top)  
  
## <a name="see-also"></a>Consulte también  
 [Partitioned Tables and Indexes](../../relational-databases/partitions/partitioned-tables-and-indexes.md)  
  
  
