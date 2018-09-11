---
title: Desempaquetar un paquete DAC | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- wizard [DAC], unpack
- data-tier application [SQL Server], unpack
- How to [DAC], unpack
- unpack DAC
ms.assetid: 697b69b3-f157-4e22-ac4e-f65c5fc2d0ad
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c6fd8dc38147cd3053aaf1720f9c3b30ea0ac512
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2018
ms.locfileid: "43810361"
---
# <a name="unpack-a-dac-package"></a>Desempaquetar un paquete de DAC
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Utilice el diálogo Unpack Data-tier Application para descomprimir los scripts y archivos de un paquete de la aplicación de capa de datos (DAC). Los scripts y archivos se colocan en una carpeta donde se pueden revisar antes de usar el paquete para implementar la DAC en un sistema de producción. El contenido de una DAC también se puede comparar con el contenido de otro paquete desempaquetado en otra carpeta.  
  
1.  **Antes de empezar:**  [Seguridad](#Security)  
  
2.  **Para desempaquetar una DAC, mediante:**  [Cuadro de diálogo Desempaquetar aplicación de capa de datos](#UnpackDACDial), [Examinar el contenido de un paquete DAC](#ExamDACPack)  
  
##  <a name="Security"></a> Seguridad  
 Se recomienda no implementar un paquete DAC desde orígenes desconocidos o que no sean de confianza. Es posible que estas DAC contengan código malintencionado que podría ejecutar código [!INCLUDE[tsql](../../includes/tsql-md.md)] no deseado o provocar errores al modificar el esquema. Antes de usar una DAC de un origen desconocido o que no es de confianza, impleméntela en una instancia de prueba aislada de [!INCLUDE[ssDE](../../includes/ssde-md.md)], desempaquete la DAC y examine el código, como los procedimientos almacenados o el código definido por el usuario.  
  
##  <a name="UnpackDACDial"></a> Cuadro de diálogo Desempaquetar aplicación de capa de datos  
 **Para desempaquetar un archivo de paquete DAC**  
  
-   En el **Explorador de Windows**, vaya a la ubicación de un archivo de paquete DAC (.dacpac).  
  
-   Use uno de estos dos métodos para abrir el cuadro de diálogo Desempaquetar aplicación de capa de datos:  
  
    1.  Haga clic con el botón derecho en el archivo de paquete DAC (.dacpac) y seleccione **Desempaquetar**.  
  
    2.  Haga doble clic en el archivo de paquete DAC.  
  
-   Complete los cuadros de diálogo:  
  
    -   [Desempaquetar archivo de paquete DAC de Microsoft SQL Server](#Unpack)  
  
    -   [Buscar carpeta](#Browse)  
  
###  <a name="Unpack"></a> Desempaquetar archivo de paquete DAC de Microsoft SQL Server  
 Use esta página para especificar la carpeta de destino en la que colocar los archivos desempaquetados y, a continuación, proceda a desempaquetar los archivos.  
  
 **Los archivos se desempaquetarán en esta carpeta:** Especifique la ruta de acceso completa a la carpeta para los archivos desempaquetados. Si la carpeta existe y conoce la ruta de acceso completa, escriba la ruta en el cuadro. Si no, haga clic en el botón **Examinar** para navegar hasta una carpeta o crear una nueva carpeta.  
  
 **Examinar** Abre la página **Buscar carpeta** donde puede seleccionar una carpeta si examina la jerarquía de archivos, o crear una nueva carpeta.  
  
 **Desempaquetar** Comienza a desempaquetar los archivos.  
  
 **Cancelar** Cierra el cuadro de diálogo sin desempaquetar el paquete DAC.  
  
###  <a name="Browse"></a> Buscar carpeta  
 Use esta página para elegir la carpeta de destino para desempaquetar los archivos. Opcionalmente, también puede crear una nueva carpeta.  
  
 **Lista de carpetas** Muestra la jerarquía de archivos del equipo. Expanda los nodos para navegar hasta la carpeta en la que desempaquetar el paquete DAC. Haga clic en la carpeta y luego en **Aceptar**.  
  
 **Crear nueva carpeta** Abre un cuadro de diálogo en el que puede especificar el nombre de una nueva carpeta que se va a crear en la carpeta que ha seleccionado en la jerarquía de carpetas.  
  
 **Aceptar** Coloca la ruta de acceso de la carpeta que seleccionó en el cuadro **Los archivos se desempaquetarán en esta carpeta** de la página **Desempaquetar archivo de paquete DAC** y le devuelve a esa página.  
  
 **Cancelar** Cierra el cuadro de diálogo sin seleccionar una carpeta.  
  
##  <a name="ExamDACPack"></a> Examinar el contenido de un paquete DAC  
 Después de desempaquetar el paquete, puede examinar los archivos generados por el cuadro de diálogo **Desempaquetar aplicación de capa de datos** . El cuadro de diálogo compila los siguientes archivos en la carpeta de destino seleccionada:  
  
1.  Un script Transact-SQL que contiene las instrucciones para crear los objetos definidos en la DAC. El nombre de archivo es *NombreDAC*.sql, donde *NombreDAC* es el nombre de la DAC.  
  
2.  Todos los archivos XML del paquete.  
  
3.  Todos los archivos de la sección de archivos adicionales de la DAC, como los archivos previos y posteriores a la implementación.  
  
 Para obtener más información, consulte [Validate a DAC Package](../../relational-databases/data-tier-applications/validate-a-dac-package.md).  
  
## <a name="see-also"></a>Ver también  
 [Aplicaciones de capa de datos](../../relational-databases/data-tier-applications/data-tier-applications.md)   
 [Implementar una aplicación de capa de datos](../../relational-databases/data-tier-applications/deploy-a-data-tier-application.md)   
 [Actualizar una aplicación de capa de datos](../../relational-databases/data-tier-applications/upgrade-a-data-tier-application.md)  
  
  
