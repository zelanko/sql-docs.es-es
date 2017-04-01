---
title: "Paso 3: Agregar redirecci&#243;n de flujo de errores | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
applies_to: 
  - "SQL Server 2016"
ms.assetid: 5683a45d-9e73-4cd5-83ca-fae8b26b488c
caps.latest.revision: 39
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
---
# Paso 3: Agregar redirecci&#243;n de flujo de errores
Como se ha mostrado en la tarea anterior, la transformación Lookup Currency Key no puede generar una coincidencia cuando la transformación intenta procesar el archivo plano de ejemplo dañado que ha generado un error. Puesto que la transformación utiliza la configuración de salida de error predeterminada, cualquier error da lugar a un error de la transformación. Cuando se produce un error en la transformación, también se produce un error en el resto del paquete.  
  
En lugar de permitir que se produzca un error en la transformación, puede configurar el componente de modo que la fila que genera el error se redirija a otra ruta de procesamiento mediante la salida de error. El uso de una ruta de procesamiento independiente permite hacer varias cosas. Por ejemplo, puede intentar eliminar los datos y luego volver a procesar la fila con error. O bien, puede guardar la fila con error junto con otra información adicional sobre el error para comprobarla y procesarla de nuevo más adelante.  
  
En esta tarea configurará la transformación Lookup Currency Key para redirigir cualquier fila con errores a la salida de errores. En la rama de errores del flujo de datos, estas filas se escribirán en un archivo.  
  
De forma predeterminada, las dos columnas adicionales en una salida de errores de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , **ErrorCode** y **ErrorColumn**, solo contienen códigos numéricos que representan un número de error y el Id. de la columna en la que se produjo el error. Estos valores numéricos pueden tener un uso limitado sin la correspondiente descripción del error.  
  
Para mejorar la utilidad de la salida de errores, antes de que el paquete escriba las filas con errores en el archivo, se utilizará un componente de script para obtener acceso a la API de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] y obtener una descripción del error.  
  
### Para configurar una salida de error  
  
1.  En el **Cuadro de herramientas de SSIS**, expanda **Comunes**y, a continuación, arrastre **Componente de script** a la superficie de diseño de la pestaña **Flujo de datos** . Coloque **Script** a la derecha de la transformación **Lookup Currency Key** .  
  
2.  En el cuadro de diálogo **Seleccionar el tipo de componente de script** , haga clic en **Transformación**y luego en **Aceptar**.  
  
3.  Haga clic en la transformación **Lookup Currency Key** y luego arrastre la flecha roja hasta la transformación **Script** que acaba de agregar para conectar los dos componentes.  
  
    La flecha roja representa la salida de errores de la transformación **Lookup Currency Key** . Utilizando la flecha roja para conectar la transformación con el componente de script, puede redirigir cualquier error de procesamiento a dicho componente, que, a continuación, lo procesará y enviará al destino.  
  
4.  En el cuadro de diálogo **Configurar la salida de errores** , en la columna **Error** , seleccione **Redirigir fila**y, a continuación, haga clic en **Aceptar**.  
  
5.  En la superficie de diseño **Flujo de datos**, haga clic en **Componente de script** en el **Componente de script** recién agregado y cambie el nombre por **Get Error Description**.  
  
6.  Haga doble clic en la transformación **Get Error Description**.  
  
7.  En el cuadro de diálogo **Editor de transformación Script** , en la página **Columnas de entrada** , seleccione la columna **ErrorCode** .  
  
8.  En la página **Entradas y salidas** , expanda **Salida 0**, haga clic en **Columnas de salida**y, a continuación, en **Agregar columna**.  
  
9. En la propiedad **Nombre**, escriba **ErrorDescription** y establezca la propiedad **DataType** en **Cadena Unicode [DT_WSTR]**.  
  
10. En la página **Script**, compruebe que la propiedad **LocaleID** esté establecida en **Inglés (Estados Unidos).**  
  
11. Haga clic en **Editar script** para abrir [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] Tools for Applications (VSTA). En el método **Input0_ProcessInputRow**, escriba o pegue el código siguiente.  
  
    [Visual Basic]  
  
    ```  
    Row.ErrorDescription =   
      Me.ComponentMetaData.GetErrorDescription(Row.ErrorCode)  
    ```  
  
    [Visual C#]  
  
    ```  
    Row.ErrorDescription = this.ComponentMetaData.GetErrorDescription(Row.ErrorCode);  
    ```  
  
    La subrutina completada será como el código siguiente.  
  
    [Visual Basic]  
  
    ```  
    Public Overrides Sub Input0_ProcessInputRow(ByVal Row As Input0Buffer)  
  
      Row.ErrorDescription =   
        Me.ComponentMetaData.GetErrorDescription(Row.ErrorCode)  
  
    End Sub  
    ```  
  
    [Visual C#]  
  
    ```  
    public override void Input0_ProcessInputRow(Input0Buffer Row)  
        {  
  
            Row.ErrorDescription = this.ComponentMetaData.GetErrorDescription(Row.ErrorCode);  
  
        }  
    ```  
  
12. En el menú **Compilar** , haga clic en **Compilar solución** para compilar el script y guardar los cambios y, a continuación, cierre VSTA.  
  
13. Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Editor de transformación Script** .  
  
## Pasos siguientes  
[Paso 4: Agregar un destino de archivo plano](../integration-services/step-4-adding-a-flat-file-destination.md)  
  
  
  
