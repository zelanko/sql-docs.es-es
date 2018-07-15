---
title: Preparar para consultar datos modificados | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- incremental load [Integration Services],preparing query
ms.assetid: 9ea2db7a-3dca-4bbf-9903-cccd2d494b5f
caps.latest.revision: 26
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 88f2dd6e5caf6cf5b601f07ca826d85808f9e6f9
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37248815"
---
# <a name="prepare-to-query-for-the-change-data"></a>Preparar para consultar datos modificados
  En el flujo de control de un paquete de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que realiza una carga incremental de datos modificados, la tercera y última tarea consiste en preparar la consulta de los datos modificados y agregar una tarea Flujo de datos.  
  
> [!NOTE]  
>  La segunda tarea para el flujo de control consiste en asegurarse de que están listos los datos modificados para el intervalo seleccionado. Para obtener más información sobre esta tarea, vea [Determinar si los datos modificados están preparados](determine-whether-the-change-data-is-ready.md). Para obtener una descripción del proceso general de diseño del flujo de control, vea [Captura de datos modificados &#40;SSIS&#41;](change-data-capture-ssis.md).  
  
## <a name="design-considerations"></a>Consideraciones de diseño  
 Para recuperar los datos modificados, se llama a una función con valores de tabla de Transact-SQL que acepta los extremos del intervalo como parámetros de entrada y devuelve los datos modificados para el intervalo especificado. Un componente de origen del flujo de datos llama a esta función. Para obtener información sobre este componente de origen, vea [Recuperar y describir datos modificados](retrieve-and-understand-the-change-data.md).  
  
 Los componentes de origen de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que se han usado con más frecuencia, como son el origen de OLE DB, el origen de ADO y el origen de ADO NET, no pueden derivar información de parámetros para una función con valores de tabla. Por consiguiente, la mayoría de los orígenes no pueden llamar directamente a una función con parámetros.  
  
 Dispone de dos opciones de diseño para pasar los parámetros de entrada a la función:  
  
-   **Ensamblar la consulta con parámetros como una cadena**. Puede utilizar una tarea Script o una tarea Ejecutar SQL para ensamblar una cadena SQL dinámica cuyos valores de parámetros estén codificados de forma rígida en la cadena. A continuación, puede almacenar esta cadena en una variable de paquete y utilizarla para establecer la propiedad SqlCommand de un componente de origen. Este enfoque tiene éxito porque el componente de origen ya no requiere la información de los parámetros.  
  
    > [!NOTE]  
    >  Un script precompilado produce menos sobrecarga que una tarea Ejecutar SQL.  
  
-   **Utilizar un contenedor con parámetros**. También puede crear un procedimiento almacenado con parámetros como un contenedor que llama a la función con valores de tabla con parámetros. Este enfoque tiene éxito porque un componente de origen puede derivar correctamente la información de parámetros para un procedimiento almacenado.  
  
 En este tema se utiliza la primera opción de diseño y se ensambla una consulta con parámetros como una cadena.  
  
## <a name="preparing-the-query"></a>Preparar la consulta  
 Antes de poder concatenar los valores de los parámetros de entrada en una sola cadena de consulta, se deben establecer las variables de paquete necesarias para la consulta.  
  
#### <a name="to-set-up-package-variables"></a>Para establecer las variables de paquetes  
  
-   En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], en la ventana **Variables** , cree una variable con un tipo de datos de cadena para guardar la cadena de consulta devuelta por la tarea Ejecutar SQL.  
  
     En este ejemplo se utiliza el nombre de variable SqlDataQuery.  
  
 Una vez creada la variable de paquete, puede utilizar una tarea Script o una tarea Ejecutar SQL para concatenar los valores de los parámetros de entrada. En los dos procedimientos siguientes se describe cómo configurar estos componentes.  
  
#### <a name="to-use-a-script-task-to-concatenate-the-query-string"></a>Para utilizar una tarea Script para concatenar la cadena de consulta  
  
1.  En la pestaña **Flujo de control** , agregue una tarea Script al paquete después del contenedor de bucles For y conecte dicho contenedor a la tarea.  
  
    > [!NOTE]  
    >  En este procedimiento se supone que el paquete realiza una carga incremental desde una única tabla. Si el paquete carga de varias tablas y tiene un paquete primario con varios paquetes secundarios, esta tarea se agregaría como primer componente a cada paquete secundario. Para obtener más información, vea [Realizar una carga incremental de varias tablas](perform-an-incremental-load-of-multiple-tables.md).  
  
2.  En el **Editor de la tarea Script**, en la página **Script** , seleccione las opciones siguientes:  
  
    1.  Para **ReadOnlyVariables**, seleccione **User::DataReady**, **User::ExtractStartTime**y **User::ExtractEndTime** en la lista.  
  
    2.  Para **ReadWriteVariables**, seleccione User::SqlDataQuery en la lista.  
  
3.  En el **Editor de la tarea Script**, en la página **Script** , haga clic en **Modificar script** para abrir el entorno de desarrollo de script.  
  
4.  En el procedimiento Main, escriba uno de los segmentos de código siguientes:  
  
    -   Si está programando en C#, escriba las líneas de código siguientes:  
  
        ```  
        int dataReady;  
        System.DateTime extractStartTime;  
        System.DateTime extractEndTime;  
        string sqlDataQuery;  
  
        dataReady = (int)Dts.Variables["DataReady"].Value;  
        extractStartTime = (System.DateTime)Dts.Variables["ExtractStartTime"].Value;  
        extractEndTime = (System.DateTime)Dts.Variables["ExtractEndTime"].Value;  
  
        if (dataReady == 2)  
          {  
          sqlDataQuery = "SELECT * FROM CDCSample.uf_Customer('" + string.Format("{0:yyyy-MM-dd hh:mm:ss}", extractStartTime) + "', '" + string.Format("{0:yyyy-MM-dd hh:mm:ss}", extractEndTime) + "')";  
          }  
        else  
          {  
          sqlDataQuery = "SELECT * FROM CDCSample.uf_Customer(null" + ", '" + string.Format("{0:yyyy-MM-dd hh:mm:ss}", extractEndTime) + "')";  
          }  
  
        Dts.Variables["SqlDataQuery"].Value = sqlDataQuery;  
        ```  
  
         \- O bien  
  
    -   Si está programando en [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)], escriba las líneas de código siguientes:  
  
        ```  
        Dim dataReady As Integer  
        Dim extractStartTime As Date  
        Dim extractEndTime As Date  
        Dim sqlDataQuery As String  
  
        dataReady = CType(Dts.Variables("DataReady").Value, Integer)  
        extractStartTime = CType(Dts.Variables("ExtractStartTime").Value, Date)  
        extractEndTime = CType(Dts.Variables("ExtractEndTime").Value, Date)  
  
        If dataReady = 2 Then  
          sqlDataQuery = "SELECT * FROM CDCSample.uf_Customer('" & _  
              String.Format("{0:yyyy-MM-dd hh:mm:ss}", extractStartTime) & _  
              "', '" & _  
              String.Format("{0:yyyy-MM-dd hh:mm:ss}", extractEndTime) & _  
              "')"  
        Else  
          sqlDataQuery = "SELECT * FROM CDCSample.uf_Customer(null" & _  
              ", '" & _  
              String.Format("{0:yyyy-MM-dd hh:mm:ss}", extractEndTime) & _  
              "')"  
        End If  
  
        Dts.Variables("SqlDataQuery").Value = sqlDataQuery  
  
        ```  
  
5.  Deje la línea de código que devuelve predeterminada `DtsExecResult.Success` de la ejecución de la secuencia de comandos.  
  
6.  Cierre el entorno de desarrollo de script y el **Editor de la tarea Script**.  
  
#### <a name="to-use-an-execute-sql-task-to-concatenate-the-query-string"></a>Para utilizar una tarea Ejecutar SQL para concatenar la cadena de consulta  
  
1.  En la pestaña **Flujo de control** , agregue una tarea Ejecutar SQL al paquete después del contenedor de bucles For y conecte dicho contenedor a esta tarea.  
  
    > [!NOTE]  
    >  En este procedimiento se supone que el paquete realiza una carga incremental desde una única tabla. Si el paquete carga de varias tablas y tiene un paquete primario con varios paquetes secundarios, esta tarea se agregaría como primer componente a cada paquete secundario. Para obtener más información, vea [Realizar una carga incremental de varias tablas](perform-an-incremental-load-of-multiple-tables.md).  
  
2.  En el **Editor de la tarea Ejecutar SQL**, en la página **General** , seleccione las opciones siguientes:  
  
    1.  En **Conjunto de resultados**, seleccione **Fila única**.  
  
    2.  Configure una conexión válida con una base de datos de origen.  
  
    3.  En **SQLSourceType**, seleccione **Entrada directa**.  
  
    4.  En **SQLStatement**, escriba la siguiente instrucción SQL:  
  
        ```  
        declare @ExtractStartTime datetime,  
        @ExtractEndTime datetime,   
        @DataReady int  
  
        select @DataReady = ?,   
        @ExtractStartTime = ?,   
        @ExtractEndTime = ?  
  
        if @DataReady = 2  
        select N'select * from CDCSample.uf_Customer'  
        + N'('''+ convert(nvarchar(30),@ExtractStartTime,120)  
        + ''', '''  
        + convert(nvarchar(30),@ExtractEndTime,120) + ''') '   
        as SqlDataQuery  
        else  
        select N'select * from CDCSample.uf_Customer'  
        + N'(null, '''  
        + convert(nvarchar(30),@ExtractEndTime,120)  
        + ''') '  
        as SqlDataQuery  
  
        ```  
  
        > [!NOTE]  
        >  El `else` cláusula en este ejemplo genera una consulta para la carga inicial de datos modificados pasando un valor null para la fecha y hora de inicio. En este ejemplo no se contempla el escenario en el que los cambios que se realizaron antes de habilitar la captura de datos modificados también deben cargarse en el almacenamiento de datos.  
  
3.  En la página **Asignación de parámetros** del **Editor de la tarea Ejecutar SQL**, haga la asignación siguiente:  
  
    1.  Asigne la variable DataReady al parámetro 0.  
  
    2.  Asigne la variable ExtractStartTime al parámetro 1.  
  
    3.  Asigne la variable ExtractEndTime al parámetro 2.  
  
4.  En la página **Conjunto de resultados** del **Editor de la tarea Ejecutar SQL**, asigne el nombre del resultado a la variable SqlDataQuery.  
  
     El nombre del resultado es el nombre de la única columna que se devuelve, SqlDataQuery.  
  
 Los procedimientos anteriores configuran una tarea que prepara una cadena de consulta con valores de cadena codificados de forma rígida para los parámetros de entrada. El código siguiente es un ejemplo de este tipo de cadena de consulta:  
  
 `select * from CDCSample. uf_Customer('2007-06-11 14:21:58', '2007-06-12 14:21:58')`  
  
## <a name="adding-a-data-flow-task"></a>Agregar una tarea Flujo de datos  
 El último paso para diseñar el flujo de control para el paquete consiste en agregar una tarea Flujo de datos.  
  
#### <a name="to-add-a-data-flow-task-and-complete-the-control-flow"></a>Para agregar una tarea Flujo de datos y completar el flujo de control  
  
-   En la pestaña **Flujo de control** , agregue una tarea Flujo de Datos y conecte la tarea que concatenó la cadena de consulta.  
  
## <a name="next-step"></a>Paso siguiente  
 Después de preparar la cadena de consulta y configurar la tarea Flujo de Datos, el paso siguiente consiste en crear la función con valores de tabla que recuperará los datos modificados de la base de datos.  
  
 **Próximo tema:** [Crear la función para recuperar los datos modificados](create-the-function-to-retrieve-the-change-data.md)  
  
  
