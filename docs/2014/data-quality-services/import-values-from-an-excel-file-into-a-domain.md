---
title: Importar valores desde un archivo de Excel a un dominio | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql12.dqs.kb.failingvalues.f1
- sql12.dqs.kb.importfailing.f1
- sql12.dqs.kb.importselect.f1
ms.assetid: 04cde693-2043-477f-8417-fcc463ca7195
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 74be4b3e924d02f6992b927af35c7774c3ea0ae4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "65484311"
---
# <a name="import-values-from-an-excel-file-into-a-domain"></a>Importar valores desde un archivo de Excel a un dominio
  En este tema se describe cómo importar valores desde un archivo de Excel a un dominio de [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS). El uso de un archivo de Excel para importar valores de dominio en la aplicación [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] simplifica el proceso de generación del conocimiento, lo que permite ahorrar tiempo y esfuerzo. Permite a quienes tienen una lista de valores de datos válidos en un archivo de Excel o en un archivo de texto importar dichos valores en un dominio. Desde un archivo de Excel es posible importar valores de dominio en uno o varios dominios de una base de conocimiento. (Consulte [importar dominios desde un archivo de Excel en la detección de conocimiento](../../2014/data-quality-services/import-domains-from-an-excel-file-in-knowledge-discovery.md) para obtener más información acerca de la importación de dominios en una base de conocimiento). No se admite la exportación a un archivo de Excel.  
  
 Puede importar valores de datos de dos formas:  
  
-   Cree un nuevo dominio y después importe valores en él desde un archivo de Excel, en cuyo caso se agregarán todos los valores al dominio.  
  
-   Importe los valores en un dominio existente que ya contenga valores, en cuyo caso solamente se importarán los nuevos valores. Los valores existentes no se importarán.  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Prerequisites"></a> Requisitos previos  
 Para importar dominios desde un archivo de Excel, es necesario tener instalado Excel en el equipo en el que está instalada la aplicación [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] para poder importar valores de dominio o un dominio completo; también se debe haber creado un archivo de Excel con valores de dominio (vea [How the import works](#How)), así como haber creado y abierto una base de conocimiento en la que importar el dominio.  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 Debe disponer del rol dqs_kb_editor o dqs_administrator en la base de datos DQS_MAIN para poder importar valores de dominio desde un archivo de Excel.  
  
##  <a name="Import"></a>Importar valores de un archivo de Excel a un dominio  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][Ejecute la aplicación Data Quality Client](../../2014/data-quality-services/run-the-data-quality-client-application.md).  
  
2.  En la página de inicio de [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , abra una base de conocimiento en la actividad Administración de dominios.  
  
3.  Si va a agregar valores a un nuevo dominio, cree este mediante el icono **Crear un dominio** y selecciónelo en la lista de dominios.  
  
4.  Si va a agregar valores a un dominio existente, selecciónelo en la lista de dominios.  
  
5.  Haga clic en la pestaña **Valores del dominio** , haga clic en el icono **Importar valores** de la barra de iconos y, a continuación, haga clic en **Importar valores válidos desde Excel**.  
  
6.  En el cuadro de diálogo **Importar valores del dominio** , haga clic en **Examinar**.  
  
7.  En el cuadro de diálogo **Seleccionar archivo** , desplácese a la carpeta que contiene el archivo de Excel desde el que desea importar valores de dominio, selecciónelo (con una extensión .xlsx, .xls o .csv) y haga clic en **Abrir**. El archivo debe estar ubicado en el cliente desde el que se ejecuta DQS, o en un recurso compartido de archivos al que el usuario tenga acceso.  
  
8.  En la lista desplegable **Hoja de cálculo** , seleccione la hoja de cálculo desde la que va a realizar la importación.  
  
9. Seleccione **Usar la primera fila como encabezado** si la primera fila de la hoja de cálculo representa el nombre del dominio y las restantes filas representan valores de dominio válidos.  
  
10. Haga clic en **OK**. Aparece una barra de progreso, indicando cuántos valores se han importado correctamente, cuántos no se han importado y cuál es el número total de valores. Haga clic en el botón **Cancelar** para cancelar el proceso.  
  
11. Compruebe que aparece el mensaje "Importación completada" en el cuadro de diálogo **Importar valores del dominio**. En este cuadro de diálogo podrá comprobar los valores que se han importado correctamente y los que no. Indica el nombre y la ruta de acceso del archivo, el estado de conclusión de la operación, cuántos valores se han importado correctamente, cuántos no se han importado y el número total de valores procesados.  
  
12. Para aquellos valores que no se importaron correctamente, haga clic en **Registro** para mostrar el cuadro de diálogo **Importar valores de dominio: valores con error** y ver por qué se ha producido un error en la operación de importación. La columna **Valor con error** muestra los valores que no se pudieron importar desde un archivo de Excel a un dominio, y la columna **Motivo** explica por qué se produjo un error en la importación. Haga clic en **Copiar al Portapapeles** para copiar la tabla **Valor con error** en el Portapapeles, desde donde podrá copiarla en otro programa, como una hoja de cálculo de Excel o un archivo del Bloc de notas. Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Valores con error** .  
  
13. Haga clic en **Aceptar** para completar la operación de importación y cerrar el cuadro de diálogo. Si la importación ha finalizado correctamente, la lista de valores de dominio de la página **Valores del dominio** se actualiza para incluir los nuevos valores importados. El filtro se cambia a **Todos los valores** y se selecciona **Mostrar solo nuevo** . Si se selecciona **Mostrar solo nuevo** después de realizar la operación de importación, solo se mostrarán los valores importados desde el archivo de Excel.  
  
14. Haga clic en **Finalizar** para agregar los valores a la base de conocimiento.  
  
##  <a name="FollowUp"></a>Seguimiento: después de importar valores de un archivo de Excel a un dominio  
 Una vez importados los valores en un dominio, puede realizar en él otras tareas de administración, ejecutar la detección de conocimiento para agregar conocimiento al dominio o agregar a este una directiva de coincidencia. Para más información, vea [Realizar la detección de conocimiento](../../2014/data-quality-services/perform-knowledge-discovery.md), [Administrar un dominio](../../2014/data-quality-services/managing-a-domain.md) o [Crear una directiva de coincidencia](../../2014/data-quality-services/create-a-matching-policy.md).  
  
##  <a name="Synonyms"></a>Importar sinónimos  
 Los sinónimos se importan de la manera siguiente:  
  
-   En primer lugar, se importan todos los valores y, a continuación, se establece la conexión de sinónimos.  
  
-   Si no es posible conectar los valores de sinónimo, aparecerá un error en la pantalla del registro. Es posible que los valores iniciales y los sinónimos existentes en el archivo se importen en el dominio, pero que no se establezcan como sinónimos.  
  
 Se aplican las consideraciones siguientes al proceso de establecimiento de las conexiones de sinónimos:  
  
-   Si el valor inicial del archivo de Excel ya existe en el dominio como sinónimo de un valor diferente, deberá establecer los sinónimos manualmente (por ejemplo, en el archivo de Excel deseamos que el valor A sea el valor inicial para el valor B, pero en el dominio el valor A aparece como sinónimo del valor C). Además de establecer los sinónimos manualmente una vez finalizada la importación, también es posible desvincular los valores que son sinónimos actualmente (por ejemplo, desvincular los valores A y C anteriores) y, a continuación, importar el archivo.  
  
-   Si el sinónimo ya está conectado con un valor inicial diferente, tendrá que establecer los sinónimos manualmente.  
  
-   Si, por cualquier motivo, los valores no se pueden conectar manualmente en la aplicación, las conexiones de sinónimos no se podrán aplicar durante la operación de importación.  
  
##  <a name="How"></a>Cómo funciona la importación  
 Esta operación importa los valores siguientes:  
  
 En la operación de importación, DQS importa desde un archivo de Excel de la manera siguiente:  
  
-   Se importan los valores correctos y los nuevos. Si uno o varios de los valores de dominio importados ya existen, los valores no se importarán.  
  
-   Un valor que contradice una regla de dominio se importará como un valor no válido.  
  
-   Un valor no se importará desde el archivo si no coincide con el tipo de datos del dominio o es NULL.  
  
-   Los valores se importan en el orden en que aparecen en el archivo.  
  
-   Cada fila representa un valor de dominio.  
  
-   La primera fila puede representar los nombres de dominio o el primer valor o registro de datos, dependiendo del valor de la casilla **Usar la primera fila como encabezado** . Si selecciona **Usar la primera fila como encabezado** al utilizar un archivo .xslx o .xls, los nombres de columna que sean NULL se convertirán automáticamente en F*n*, y se agregará un número a las columnas que estén duplicadas.  
  
-   Si cancela la operación de importación antes de que finalice, la operación se revertirá y no se importará ningún dato.  
  
-   Los valores de la primera columna se importan en el dominio. Si, además de la primera columna, hay una o varias columnas adicionales que contienen datos, los valores de dichas columnas se agregarán como sinónimos (vea [Importar sinónimos](#Synonyms)).  
  
    -   El formato esperado es que la primera columna contenga valores iniciales y las columnas siguientes sinónimos.  
  
    -   Puede importar varios sinónimos en la misma fila o en filas diferentes. Por ejemplo, si quiere importar "NYC" y "New York City" como sinónimos de "New York", puede importar una única fila con "New York" en la columna 1, "NYC" en la columna 2 y "New York City" en la columna 3; o bien importar una fila con "New York" en la columna 1 y "NYC" en la columna 2, y otra fila con "New York" en la columna 1 y "New York City" en la columna 2. Tenga en cuenta que si el valor "New York" ya existe en el dominio, solo se agregarán los sinónimos, y el usuario no recibirá ningún error durante el proceso de importación indicándole que el valor ya existe. Si el primer valor no existe, se agregará al dominio.  
  
 Se aplican las reglas siguientes al archivo de Excel utilizado para la importación:  
  
-   El archivo de Excel puede tener la extensión .xlsx, .xls o .csv. Es necesario tener instalado Microsoft Excel en el equipo en que está instalada la aplicación [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] para poder importar valores de dominio o un dominio completo. Se admiten las versiones 2003 y posteriores de Excel. Si se utiliza la versión de 64 bits de Excel, solo se admitirán los archivos de Excel 2003; los archivos de Excel 2007 o 2010 no son compatibles.  
  
-   Los archivos de Excel de tipo .xlsx no se admiten en una instalación de 64 bits de Excel. Si utiliza Excel de 64 bits, guarde el archivo de hoja de cálculo como un archivo .xls o .csv, o utilice una instalación de 32 bits de Excel en su lugar.  
  
-   En los archivos .xlsx y .xls, el tipo de datos de la columna está determinado por las ocho primeras filas. Si el tipo de datos existentes en las ocho primeras filas de esa columna es mixto, la columna será de tipo cadena. Si una celda de la fila 9 o superior no se ajusta a ese tipo de datos, se le asignará un valor NULL.  
  
-   En los archivos .csv, el tipo de datos está determinado por el tipo de datos más frecuente de las ocho primeras filas.  
  
-   Si el archivo de Excel no tiene el formato correcto o está dañado, la operación de importación generará un error.  
  
  
