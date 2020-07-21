---
title: 'Tarea 1: crear una base de conocimiento y dominios | Microsoft Docs'
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 7d74a60b-8933-4038-bcbb-4e9dcc4f70e9
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: f7ad3b085178c0d0cfe3ece010a571992e7fdb99
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85064862"
---
# <a name="task-1-creating-a-knowledge-base-and-domains"></a>Tarea 1: Creación de una base de conocimiento y dominios
  En esta tarea, creará la base de conocimiento **proveedores** y creará dominios que se usarán para la limpieza de datos y los datos coincidentes para quitar duplicados.  
  
1.  Inicie **Data Quality Client**. Haga clic en **Inicio**, seleccione **todos los programas**, haga clic en **Microsoft SQL Server 2012**, en **Data Quality Services**y, a continuación, haga clic en **Data Quality Client**.  
  
2.  En el cuadro de diálogo **conectar al servidor** , seleccione la instancia del servidor de bases de datos en la que está instalado DQS y haga clic en **conectar**.  
  
     ![Cuadro de diálogo conectar al servidor](../../2014/tutorials/media/et-creatingaknowledgebaseanddomains-01.jpg "Cuadro de diálogo Conectar a servidor")  
  
3.  En la Página principal de Data Quality Client, en el panel administración de la **base de conocimiento** , haga clic en **nueva base de conocimiento**.  
  
     ![Administración de bases de conocimiento - Nueva Knowledge Base](../../2014/tutorials/media/et-creatingaknowledgebaseanddomains-02.jpg "Administración de bases de conocimiento - Nueva Knowledge Base")  
  
4.  Escriba **proveedores** como **nombre** de la base de conocimiento.  
  
     ![Nueva Knowledge Base - Administración de dominios](../../2014/tutorials/media/et-creatingaknowledgebaseanddomains-03.jpg "Nueva Knowledge Base - Administración de dominios")  
  
5.  Confirme que el campo **crear base de conocimiento a partir de** está establecido en **ninguno** , ya que está creando la base de conocimiento **proveedores** desde cero.  
  
6.  Confirme que está seleccionada la opción **Administración de dominios** para la **actividad** y haga clic en **siguiente**. La actividad Administración de dominios permite crear y administrar dominios en la base de conocimiento.  
  
7.  En la ventana **Administración de dominios** , haga clic en el botón **crear un dominio** de la barra de herramientas para crear un dominio.  
  
     ![Botón de la barra de herramientas Crear dominio](../../2014/tutorials/media/et-creatingaknowledgebaseanddomains-04.jpg "Botón de la barra de herramientas Crear dominio")  
  
8.  En el cuadro de diálogo **crear dominio** , escriba **ID. de proveedor** para el **nombre de dominio**y haga clic en **Aceptar**.  
  
     ![Cuadro de diálogo Crear dominio](../../2014/tutorials/media/et-creatingaknowledgebaseanddomains-05.jpg "Cuadro de diálogo Crear dominio")  
  
9. Repita el paso anterior para crear los dominios siguientes con toda la configuración predeterminada. Para simplificar el tutorial, establezca el **tipo de datos** de todos los dominios como **cadena**. Los otros tipos de datos permitidos son: Integer, Decimal y Date. Cuando se selecciona la opción **usar valores iniciales** (valor predeterminado), todos los sinónimos se reemplazan por el valor inicial del grupo de sinónimos en la salida. Al establecer la opción **normalizar cadena** (valor predeterminado), se quitan los caracteres especiales de los valores de dominio. La opción **dar formato a la salida para** permite seleccionar el formato que se aplica cuando se generan los valores de datos en el dominio. Seleccione **Habilitar corrector ortográfico** (predeterminado) para ejecutar el corrector ortográfico en todos los valores de cadena al rellenar el dominio. La configuración de **idioma** especifica la versión de idioma del **corrector ortográfico** que desea aplicar. Seleccione **deshabilitar algoritmos de error de sintaxis** para rellenar el dominio sin comprobar si hay errores de sintaxis en los valores de cadena. Vea el tema sobre cómo [crear un dominio](https://msdn.microsoft.com/library/hh510401.aspx) en MSDN Library para obtener más detalles.  
  
    -   Nombre del proveedor  
  
    -   Dirección de correo electrónico de contacto  
  
    -   Address Line  
  
    -   City  
  
    -   State  
  
    -   País  
  
    -   Zip  
  
## <a name="next-step"></a>siguiente paso  
 [Tarea 2: Adición manual de valores de dominio](../../2014/tutorials/task-2-adding-domain-values-manually.md)  
  
  
