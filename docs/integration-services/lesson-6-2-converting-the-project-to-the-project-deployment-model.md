---
title: 'Paso 2: Convertir el proyecto al modelo de implementación de proyectos | Microsoft Docs'
ms.custom: ''
ms.date: 01/11/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 80964293-f1f5-4da7-b1fb-00ab8c30c1c5
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 0563ceff3185f856692292884fe63e79c16e4216
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/26/2019
ms.locfileid: "71295880"
---
# <a name="lesson-6-2-convert-the-project-to-the-project-deployment-model"></a>Lección 6-2: Convertir el proyecto al modelo de implementación de proyectos

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



En esta tarea se usa al Asistente para la conversión de proyectos de Integration Services para convertir el proyecto al modelo de implementación de proyectos.  
  
1.  En el menú **Proyecto**, seleccione **Convertir al modelo de implementación de proyectos**.  
  
2.  En la página **Introducción** del **Asistente para la conversión de proyectos de Integration Services**, revise los pasos y seleccione **Siguiente**.  
  
3.  En la página **Seleccionar paquetes**, en la lista **Paquetes**, desactive todas las casillas excepto **Lesson 6.dtsx** y seleccione **Siguiente**.  
  
4.  En la página **Especificar propiedades del proyecto**, seleccione **Siguiente**.  
  
5.  En la página **Actualizar tarea Ejecutar paquete**, seleccione **Siguiente**.  
  
6.  En la página **Seleccionar configuraciones**, asegúrese de que el paquete **Lesson 6.dtsx** está seleccionado en la lista **Configuraciones** y seleccione **Siguiente**.  
  
7.  En la página **Crear parámetros**, asegúrese de que el paquete **Lesson 6.dtsx** está seleccionado.  Compruebe que el **Ámbito** es **Paquete** en la lista **Propiedades de configuración** y luego seleccione **Siguiente**.  
  
8.  En la página **Configurar parámetros**, compruebe que los valores de **Nombre** y **Valor** son los mismos especificados en la lección 5 para la variable y el valor de configuración y seleccione **Siguiente**.  
  
9. En la página **Revisar**, en el panel **Resumen**, tenga en cuenta que el asistente ha usado la información del archivo de configuración para establecer las **Propiedades** que se van a convertir.  
  
10. Seleccione **Convertir**.  
  
    Una vez finalizada la conversión, aparece un mensaje de advertencia de que los cambios no se guardan hasta que se guarda el proyecto. Seleccione **Aceptar** para cerrar el cuadro de diálogo de advertencia.  
  
11. En el **Asistente para la conversión de proyectos de Integration Services**, seleccione **Cerrar**.  
  
12. En **SQL Server Data Tools**, seleccione el menú **Archivo** y luego **Guardar** para guardar el paquete convertido.  
  
13. Seleccione la pestaña **Parámetros** y compruebe que el paquete ya contiene un parámetro para **VarFolderName**. Ese valor de parámetro es la misma ruta de acceso especificada para la carpeta **Nuevos datos de ejemplo** en el archivo de configuración de la lección 5.  
  
## <a name="go-to-next-task"></a>Ir a la tarea siguiente
[Paso 3: Probar el paquete de la lección 6](../integration-services/lesson-6-3-testing-the-lesson-6-package.md)  
  
  
  
