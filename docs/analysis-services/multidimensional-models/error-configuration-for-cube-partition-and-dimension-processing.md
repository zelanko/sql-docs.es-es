---
title: Configuración de errores de procesamiento de dimensiones, particiones y cubos | Documentos de Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e3e8d6fe3f118709086328e4cd11a36a7ce2936d
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="error-configuration-for-cube-partition-and-dimension-processing"></a>Configuración de errores de procesamiento de dimensiones, particiones y cubos
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Las propiedades de configuración de errores de objetos de cubo, partición o dimensión determinan cómo responde el servidor cuando se producen errores de integridad de datos durante el procesamiento. Claves duplicadas, claves que faltan y valores NULL en una columna de clave suelen desencadenar esos errores, y mientras el registro que produce el error no se agregue a la base de datos, puede establecer las propiedades que determinan qué ocurre después. De forma predeterminada, el procesamiento se detiene. Sin embargo, durante el desarrollo de un cubo, puede ser conveniente que el procesamiento continúe cuando se produzcan errores para que pueda probar los comportamientos del cubo con datos importados, aunque sean incompletos.  
  
 En este tema se incluyen las secciones siguientes:  
  
-   [Orden de ejecución](#bkmk_exec)  
  
-   [Comportamientos predeterminados](#bkmk_default)  
  
-   [Propiedades de configuración de errores](#bkmk_props)  
  
-   [Dónde establecer propiedades de configuración de errores](#bkmk_tools)  
  
-   [Claves que faltan (KeyNotFound)](#bkmk_missing)  
  
-   [Claves externas NULL en una tabla de hechos (KeyNotFound)](#bkmk_nullfact)  
  
-   [Claves NULL en una dimensión](#bkmk_nulldim)  
  
-   [Claves duplicadas que producen relaciones incoherentes (KeyDuplicate)](#bkmk_dupe)  
  
-   [Cambiar el límite de errores o la acción del límite de errores](#bkmk_limit)  
  
-   [Establecer la ruta de acceso del registro de errores](#bkmk_log)  
  
-   [Paso siguiente](#bkmk_next)  
  
##  <a name="bkmk_exec"></a> Orden de ejecución  
 El servidor ejecuta siempre las reglas de **NullProcessing** antes que las reglas de **ErrorConfiguration** para cada registro. Es importante entenderlo porque las propiedades de procesamiento de valores NULL que convierten valores NULL en ceros pueden insertar posteriormente errores de clave duplicada cuando dos o más registros de error tienen cero en una columna de clave.  
  
##  <a name="bkmk_default"></a> Comportamientos predeterminados  
 De forma predeterminada, el procesamiento se detiene en el primer error que afecta a una columna de clave. Este comportamiento se controla mediante un límite de errores que especifica cero como el número de errores permitidos y la directiva Detener el procesamiento que indica al servidor que detenga el procesamiento cuando se alcanza el límite de errores.  
  
 Los registros que desencadenan un error, debido a valores NULL, que faltan o están duplicados, se convierten al miembro desconocido o se descartan. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no importará datos que infrinjan las restricciones de integridad de datos.  
  
-   La conversión al miembro desconocido se realiza de forma predeterminada, debido al valor **ConvertToUnknown** establecido para **KeyErrorAction**. Los registros asignados al miembro desconocido se ponen en cuarentena en la base de datos como prueba de un problema que puede ser conveniente investigar después de que finalice el procesamiento.  
  
     Los miembros desconocidos se excluyen de las cargas de trabajo de consulta, pero serán visibles en algunas aplicaciones cliente si **UnknownMember** se establece en **Visible**.  
  
     Si desea hacer un seguimiento de cuántos valores NULL se convirtieron al miembro desconocido, puede modificar la propiedad **NullKeyConvertedToUnknown** para notificar estos errores en el registro o en la ventana Procesamiento.  
  
-   Se descarta cuando se establece manualmente la propiedad **KeyErrorAction** en **DiscardRecord**.  
  
 Con las propiedades de configuración de errores, puede determinar cómo responde el servidor cuando se produce un error. Entre las opciones se incluyen detener el procesamiento inmediatamente, continuar con el procesamiento pero detener el registro o continuar con el procesamiento y el registro de errores. Los valores predeterminados varían en función de la gravedad del error.  
  
 El número de errores hace un seguimiento de cuántos errores se producen. Cuando se establece un límite superior, la respuesta del servidor cambia cuando se alcanza ese límite. De forma predeterminada, el servidor detiene el procesamiento cuando se llega al límite. El límite predeterminado es 0, lo que hace que el procesamiento se detenga en el primer error que se cuenta.  
  
 Los errores de mucho impacto, como una clave que falta o un valor NULL en un campo de clave, se deben resolver rápidamente. De forma predeterminada, estos errores cumplen con los comportamientos del servidor **ReportAndContinue** , donde el servidor detecta el error, lo agrega al número de errores y, después, continúa con el procesamiento (excepto si el límite de errores es cero, lo que detiene el procesamiento inmediatamente).  
  
 Hay otros errores que se generan, pero no se contabilizan ni se registran de forma predeterminada (el valor **IgnoreError** ), ya que el error no plantea necesariamente un problema de integridad de datos.  
  
 Los recuentos de errores se ven afectados por las opciones de procesamiento de valores NULL. Para los atributos de dimensión, las opciones de procesamiento de valores NULL determinan cómo responde el servidor cuando se encuentran valores NULL. De forma predeterminada, los valores NULL de una columna numérica se convierten en ceros, mientras que los valores NULL de una columna de cadenas se procesan como cadenas en blanco. Puede invalidar las propiedades **NullProcessing** para detectar los valores NULL antes de que se conviertan en errores **KeyNotFound** o **KeyDuplicate** . Para obtener información detallada, vea [Claves NULL en una dimensión](#bkmk_nulldim) .  
  
 Los errores se registran en el cuadro de diálogo Procesar, pero no se guardan. Puede especificar un nombre de archivo de registro de errores de clave para recopilar los errores en un archivo de texto.  
  
##  <a name="bkmk_props"></a> Propiedades de configuración de errores  
 Hay nueve propiedades de configuración de errores. Cinco de ellas se emplean para determinar la respuesta del servidor cuando se produce un error específico. Las otras cuatro quedan fuera del ámbito de las cargas de trabajo de configuración de errores, como el número de errores que se van a permitir, qué hacer cuando se alcance ese límite y si se van a recopilar los errores en un archivo de registro.  
  
 **Respuesta del servidor a errores concretos**  
  
|Propiedad|Valor de DB-Library|Otros valores|  
|--------------|-------------|------------------|  
|**CalculationError**<br /><br /> Se produce al inicializar la configuración de errores.|**IgnoreError** no registra ni cuenta el error; el procesamiento continúa siempre y cuando el recuento de errores esté por debajo del límite máximo.|**ReportAndContinue** registra y cuenta el error.<br /><br /> **ReportAndStop** notifica el error y detiene el procesamiento inmediatamente, cualquiera que sea el límite de errores.|  
|**KeyNotFound**<br /><br /> Se produce cuando una clave externa de una tabla de hechos no tiene una clave principal coincidente en una tabla de dimensiones relacionada (por ejemplo, una tabla de hechos Ventas tiene un registro con un identificador de producto que no existe en la tabla de dimensión Producto). Este error puede producirse durante el procesamiento de particiones o durante el procesamiento de dimensiones de copo de nieve.|**ReportAndContinue** registra y cuenta el error.|**ReportAndStop** notifica el error y detiene el procesamiento inmediatamente, cualquiera que sea el límite de errores.<br /><br /> **IgnoreError** no registra ni cuenta el error; el procesamiento continúa siempre y cuando el recuento de errores esté por debajo del límite máximo. Los registros que desencadenan este error se convierten al miembro desconocido de forma predeterminada, pero puede cambiar la propiedad **KeyErrorAction** para que se descarten en su lugar.|  
|**KeyDuplicate**<br /><br /> Se produce cuando se encuentran claves de atributo duplicadas en una dimensión. En la mayoría de los casos, es aceptable tener claves de atributos duplicadas, pero este error le informa de los duplicados para que pueda comprobar posibles errores de diseño de la dimensión que puedan provocar relaciones incoherentes entre atributos.|**IgnoreError** no registra ni cuenta el error; el procesamiento continúa siempre y cuando el recuento de errores esté por debajo del límite máximo.|**ReportAndContinue** registra y cuenta el error.<br /><br /> **ReportAndStop** notifica el error y detiene el procesamiento inmediatamente, cualquiera que sea el límite de errores.|  
|**NullKeyNotAllowed**<br /><br /> Se produce cuando se establece **NullProcessing**  =  **Error** en un atributo de dimensión o cuando existen valores NULL en una columna de clave de atributo usada para identificar un miembro de forma única.|**ReportAndContinue** registra y cuenta el error.|**ReportAndStop** notifica el error y detiene el procesamiento inmediatamente, cualquiera que sea el límite de errores.<br /><br /> **IgnoreError** no registra ni cuenta el error; el procesamiento continúa siempre y cuando el recuento de errores esté por debajo del límite máximo. Los registros que desencadenan este error se convierten al miembro desconocido de forma predeterminada, pero puede establecer la propiedad **KeyErrorAction** para que se descarten en su lugar.|  
|**NullKeyConvertedToUnknown**<br /><br /> Se produce cuando los valores NULL se convierten posteriormente al miembro desconocido. Al establecer **NullProcessing** = **ConvertToUnknown** en un atributo de dimensión, se desencadenará este error.|**IgnoreError** no registra ni cuenta el error; el procesamiento continúa siempre y cuando el recuento de errores esté por debajo del límite máximo.|Si considera que este error es informativo, mantenga el valor predeterminado. De lo contrario, puede elegir **ReportAndContinue** para notificar el error a la ventana Procesamiento y contar el error de cara al límite de errores.<br /><br /> **ReportAndStop** notifica el error y detiene el procesamiento inmediatamente, cualquiera que sea el límite de errores.|  
  
 **Propiedades generales**  
  
|**Propiedad**|**Valores**|  
|------------------|----------------|  
|**KeyErrorAction**|Es la acción que realiza el servidor cuando se produce un error de **KeyNotFound** . Entre las respuestas válidas a este error se incluyen **ConvertToUnknown** o **DiscardRecord**.|  
|**KeyErrorLogFile**|Es un nombre de archivo definido por el usuario que debe tener una extensión de archivo .log, situado en una carpeta para la que la cuenta de servicio tiene permisos de lectura y escritura. Este archivo de registro solo contendrá errores generados durante el procesamiento. Use la Caja negra si necesita información más detallada.|  
|**KeyErrorLimit**|Es el número máximo de errores de integridad de datos que el servidor permitirá antes de que se produzca un error de procesamiento. Un valor de -1 indica que no hay ningún límite. El valor predeterminado es 0, lo que significa que el procesamiento se detiene después de producirse el primer error. También puede establecerlo en un número entero.|  
|**KeyErrorLimitAction**|Es la acción que realiza el servidor cuando el número de errores de clave alcanza el límite superior. Con **Detener el procesamiento**, el procesamiento finaliza inmediatamente. Con **Detener el registro**, el procesamiento continúa pero ya no se notifican o se cuentan los errores.|  
  
##  <a name="bkmk_tools"></a> Dónde establecer propiedades de configuración de errores  
 Use las páginas de propiedades de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] una vez implementada la base de datos o del proyecto de modelo de [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]. Las mismas propiedades se encuentran en ambas herramientas. También puede establecer las propiedades de configuración de errores en el archivo msmdrsrv.ini para cambiar los valores predeterminados de configuración de errores, y en los comandos **Batch** y **Process** si el procesamiento se ejecuta como un operación de script.  
  
 Puede establecer la configuración de errores en cualquier objeto que se pueda procesar como una operación independiente.  
  
#### <a name="sql-server-management-studio"></a>SQL Server Management Studio  
  
1.  En el Explorador de objetos, haga clic con el botón derecho en **Propiedades** en uno de estos objetos: dimensión, cubo o partición.  
  
2.  En Propiedades, haga clic en **Configuración de errores**.  
  
#### <a name="sql-server-data-tools"></a>SQL Server Data Tools  
  
1.  En el Explorador de soluciones, haga doble clic en una dimensión o en un cubo. Aparece**ErrorConfiguration** en Propiedades, en el panel inferior.  
  
2.  O bien, para una única dimensión, haga clic con el botón derecho en la dimensión del Explorador de soluciones, elija **Procesar**y, después, elija **Cambiar configuración** en el cuadro de diálogo Procesar dimensión. Las opciones de configuración de errores aparecen en la pestaña Errores de clave de dimensión.  
  
##  <a name="bkmk_missing"></a> Claves que faltan (KeyNotFound)  
 Los registros en los que falta un valor de clave no se pueden agregar a la base de datos, ni siquiera cuando se pasan por alto los errores o cuando el límite de errores es ilimitado.  
  
 El servidor genera el error **KeyNotFound** durante el procesamiento de particiones, cuando un registro de la tabla de hechos contiene un valor de clave externa, pero la clave externa no tiene ningún registro correspondiente en una tabla de dimensiones relacionada. Este error también se produce al procesar tablas de dimensiones relacionadas o de copo de nieve, donde un registro de una dimensión especifica una clave externa que no existe en la dimensión relacionada.  
  
 Si se produce un error **KeyNotFound** , el registro incorrecto se asigna al miembro desconocido. Este comportamiento se controla estableciendo **Acción de clave**en **ConvertToUnknown**, de forma que pueda ver los registros asignados para investigarlos más adelante.  
  
##  <a name="bkmk_nullfact"></a> Claves externas NULL en una tabla de hechos (KeyNotFound)  
 De forma predeterminada, un valor NULL en una columna de clave externa de una tabla de hechos se convierte en cero. Suponiendo que cero no sea un valor de clave externa válido, el error **KeyNotFound** se registrará y contará de cara al límite de errores, que es cero de forma predeterminada.  
  
 Para permitir que el procesamiento continúe, puede administrar el valor NULL antes de que se convierta y se compruebe la existencia de errores. Para ello, establezca **NullProcessing** en **Error**.  
  
#### <a name="set-nullprocessing-property-on-a-measure"></a>Establecer la propiedad NullProcessing en una medida  
  
1.  En SQL Server Data Tools, en el Explorador de soluciones, haga doble clic en el cubo para abrirlo en el Diseñador de cubos.  
  
2.  Haga clic con el botón derecho en una medida del panel Medidas y elija **Propiedades**.  
  
3.  En Propiedades, expanda **Origen** para ver la propiedad **NullProcessing** . Está establecida en **Automático** de forma predeterminada, que para los elementos OLAP, convierte los valores NULL en ceros para los campos que contienen datos numéricos.  
  
4.  Cambie el valor a **Error** para excluir los registros que contienen un valor NULL, lo que impide la conversión de NULL a un número (cero). Esta modificación permite evitar los errores de clave duplicada relacionados con varios registros que tienen cero en la columna de clave y, además, evita los errores **KeyNotFound** cuando una clave externa con un valor cero no tiene ningún equivalente de clave principal en una tabla de dimensiones relacionada.  
  
##  <a name="bkmk_nulldim"></a> Claves NULL en una dimensión  
 Para continuar con el procesamiento cuando se encuentran valores NULL en claves externas en una dimensión de copo de nieve, controle los valores NULL primero estableciendo **NullProcessing** en la **KeyColumn** del atributo de dimensión. Esto descarta o convierte el registro, antes de que pueda producirse el error **KeyNotFound** .  
  
 Tiene dos opciones para administrar los valores NULL en un atributo de dimensión:  
  
-   Establecer **NullProcessing**=**UnknownMember** para asignar los registros con valores NULL al miembro desconocido. Esto genera el error **NullKeyConvertedToUnknown** , que se pasa por alto de forma predeterminada.  
  
-   Establecer **NullProcessing**=**Error** para excluir los registros que tienen valores NULL. Esto genera el error **NullKeyNotAllowed** , que se registra y cuenta de cara al límite de errores. Puede establecer la propiedad de configuración de errores **Clave NULL no permitida** en **IgnoreError** para permitir que el procesamiento continúe.  
  
 Los valores NULL pueden ser un problema en los campos que no son de clave, en los que las consultas MDX devuelven resultados diferentes en función de si NULL se interpreta como cero o como un valor vacío. Por esta razón, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] proporciona opciones de procesamiento de valores NULL que le permiten predefinir el comportamiento de conversión que desea. Para obtener información detallada, vea [Definir las propiedades de miembro desconocido y de procesamiento de valores NULL](../../analysis-services/lesson-4-7-defining-the-unknown-member-and-null-processing-properties.md) y <xref:Microsoft.AnalysisServices.NullProcessing> .  
  
#### <a name="set-nullprocessing-property-on-a-dimension-attribute"></a>Establecer la propiedad NullProcessing en un atributo de dimensión  
  
1.  En SQL Server Data Tools, en el Explorador de soluciones, haga doble clic en la dimensión para abrirla en el Diseñador de dimensiones.  
  
2.  Haga clic con el botón derecho en un atributo en el panel Atributos y elija **Propiedades**.  
  
3.  En Propiedades, expanda **KeyColumns** para ver la propiedad **NullProcessing** . Está establecida en **Automático** de forma predeterminada, lo que convierte los valores NULL en ceros para los campos que contienen datos numéricos. Cambie el valor a **Error** o **UnknownMember**.  
  
     Esta modificación quita las condiciones subyacentes que desencadenan **KeyNotFound** descartando o convirtiendo el registro antes de que se compruebe si hay errores.  
  
     En función de la configuración de errores, cualquiera de estas acciones puede producir un error que se notifica y se cuenta. Es posible que necesite ajustar otras propiedades adicionales, como establecer **KeyNotFound** en **ReportAndContinue** o **KeyErrorLimit** en un valor distinto de cero, para permitir que el procesamiento continúe cuando se notifican y se contabilizan estos errores.  
  
##  <a name="bkmk_dupe"></a> Claves duplicadas que producen relaciones incoherentes (KeyDuplicate)  
 De forma predeterminada, la presencia de una clave duplicada no detiene el procesamiento, pero el error se omite y el registro duplicado se excluye de la base de datos.  
  
 Para cambiar este comportamiento, establezca **KeyDuplicate** en **ReportAndContinue** o **ReportAndStop** para notificar el error. Puede examinar después el error para determinar si hay posibles errores en el diseño de la dimensión.  
  
##  <a name="bkmk_limit"></a> Cambiar el límite de errores o la acción del límite de errores  
 Puede aumentar el límite de errores para permitir más errores durante el procesamiento. No hay ninguna instrucción en cuanto a cómo elevar el límite de errores; el valor adecuado variará según el escenario. Los límites de errores se especifican como **KeyErrorLimit** en las propiedades **ErrorConfiguration** properties en las propiedades [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], o como **Número de errores** en las propiedades the Error Configuration tab for properties of dimensions, cubes, or measure groups en las propiedades [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 Una vez alcanzado el límite de errores, puede especificar que el procesamiento se detenga o que el registro se detenga. Por ejemplo, imagine que establece la acción en **StopLogging** en un límite de errores de 100. En el error número 101, el procesamiento continúa pero ya no se registran o se cuentan los errores. Los límites de errores se especifican como **KeyErrorLimitAction** en las propiedades **ErrorConfiguration** en [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], o como **Acción si hay error** en la pestaña Configuración de las propiedades de dimensiones, cubos o grupos de medida en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
##  <a name="bkmk_log"></a> Establecer la ruta de acceso del registro de errores  
 Puede especificar un archivo para almacenar los mensajes de error relacionados con la clave que se notifican durante el procesamiento. De forma predeterminada, los errores son visibles durante el procesamiento interactivo en la ventana Procesar y se descartan cuando se cierra la ventana o la sesión. El registro solo contendrá información de error relacionada con las claves, igual que los errores que se notifican en los cuadros de diálogo de procesamiento.  
  
 Los errores se registran en un archivo de texto que tener la extensión de archivo .log. El archivo estará vacío salvo que se produzcan errores. De forma predeterminada, el archivo se crea en la carpeta DATA. Puede especificar otra carpeta siempre y cuando la cuenta de servicio de Analysis Services pueda escribir en esa ubicación.  
  
##  <a name="bkmk_next"></a> Paso siguiente  
 Decida si los errores detendrán el procesamiento o se omitirán. Recuerde que solo se omite el error. El registro que produjo el error no se pasa por alto; se descarta o se convierte al miembro desconocido. Los registros que infringen las reglas de integridad de datos nunca se agregan a la base de datos. De forma predeterminada, el procesamiento se detiene cuando se produce el primer error, pero puede cambiar este comportamiento si aumenta el límite de errores. En el desarrollo de un cubo, puede ser útil relajar las reglas de configuración de errores, permitiendo que el procesamiento continúe, de modo que haya datos para probar.  
  
 Decida si desea cambiar los comportamientos predeterminados de procesamiento de valores NULL. De forma predeterminada, los valores NULL de una columna de cadenas se procesan como valores vacíos, mientras que los valores NULL de una columna numérica se procesan como ceros. Vea [Definir las propiedades de miembro desconocido y de procesamiento de valores NULL](../../analysis-services/lesson-4-7-defining-the-unknown-member-and-null-processing-properties.md) para obtener instrucciones sobre cómo establecer el procesamiento de valores NULL en un atributo.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades de registro](../../analysis-services/server-properties/log-properties.md)   
 [Definir el miembro desconocido y propiedades de procesamiento de valores Null](../../analysis-services/lesson-4-7-defining-the-unknown-member-and-null-processing-properties.md)  
  
  
