---
title: Ayuda F1 del Visor de archivos de registro | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.swb.configurelogs.errorlog.f1
helpviewer_keywords:
- Log File Viewer
ms.assetid: 2243845c-4880-4aa0-9ee8-0a97a128996b
caps.latest.revision: 37
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 6567e82fb59ebcad2464310811ccd97e6f67de6c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36111137"
---
# <a name="log-file-viewer-f1-help"></a>Ayuda F1 del Visor de archivos de registro
  El Visor de archivos de registro muestra información de registro de muchos componentes diferentes. Cuando el Visor del archivo de registros esté abierto, utilice el panel **Seleccionar registros** para seleccionar los registros que desea que se muestren. Cada registro muestra las columnas apropiadas a ese tipo de registro.  
  
 La disponibilidad de los registros dependerá del modo en que se abra el Visor del archivo de registros. Para obtener más información, vea [Abrir el Visor de archivos de registro](open-log-file-viewer.md).  
  
 El número de filas que se muestran para los registros de auditoría se puede configurar en la página **Explorador de objetos de SQL Server/Comandos** del cuadro de diálogo **Herramientas/Opciones**. Para obtener la descripción de las columnas que se muestran para los registros de auditoría, vea [sys.fn_get_audit_file &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/sys-fn-get-audit-file-transact-sql).  
  
## <a name="options"></a>Opciones  
 **Cargar registro**  
 Abre un cuadro de diálogo donde puede especificar un archivo de registro para cargar.  
  
 **Exportar**  
 Abre un cuadro de diálogo que permite exportar la información que se muestra en la cuadrícula **Resumen de archivos de registro** a un archivo de texto.  
  
 **Actualizar**  
 Actualice la vista de los registros seleccionados. El botón **Actualizar** hace que se vuelvan a leer los registros seleccionados del servidor de destino al tiempo que se aplica una configuración de filtro.  
  
 **Filtro**  
 Abre un cuadro de diálogo que permite especificar la configuración que se usa para filtrar el archivo de registro, como **Conexión**, **Fecha**u otros criterios de filtro de **General** .  
  
 **Buscar**  
 Permite buscar texto específico en el archivo de registro. No se admite la búsqueda con caracteres comodín.  
  
 **Detener**  
 Detiene la carga de las entradas del archivo de registro. Por ejemplo, puede utilizar esta opción si la carga de un archivo de registro remoto o sin conexión tarda mucho tiempo y solo desea ver las entradas más recientes.  
  
 **Resumen de archivos de registro**  
 Este panel de información muestra un resumen del filtro del archivo de registro. Si no se ha filtrado el archivo, se mostrará el siguiente texto: **No se aplicó ningún filtro**. Si se aplica un filtro al registro, se mostrará el texto **Filtrar entradas del registro en:** \<criteriosDeFiltro>.  
  
 **Detalles de las filas seleccionadas**  
 Seleccione una fila para mostrar detalles adicionales sobre la fila de evento seleccionada en la parte inferior de la página. Puede ordenar de nuevo las columnas arrastrándolas a nuevas ubicaciones de la cuadrícula. Puede modificar el tamaño de las columnas arrastrando las barras de separación de las columnas del encabezado de la cuadrícula hacia la izquierda o hacia la derecha. Haga doble clic en las barras de separación de las columnas del encabezado de la cuadrícula para ajustar automáticamente el tamaño de la columna al ancho del contenido.  
  
 **Instancia**  
 Nombre de la instancia en que se produjo el evento. Esto se muestra como *nombre de equipo*\\*nombre de instancia*.  
  
## <a name="frequently-displayed-columns"></a>Columnas que se muestran con frecuencia  
 **Fecha**  
 Muestra la fecha del evento.  
  
 **Source**  
 Muestra la característica de origen desde la que se crea el evento, como el nombre del servicio (MSSQLSERVER, por ejemplo). No aparece para todos los tipos de registro.  
  
 **de mensaje**  
 Muestra todos los mensajes asociados al evento.  
  
 **Tipo de registro**  
 Muestra el tipo de registro al que pertenece el evento. Todos los registros seleccionados aparecen en la ventana de resumen del archivo de registro.  
  
 **Origen del registro**  
 Muestra una descripción del registro de origen en el que se captura el evento.  
  
## <a name="permissions"></a>Permisos  
 Para tener acceso a los archivos de registro en instancias de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en línea, se requiere pertenecer al rol fijo de servidor securityadmin.  
  
 Para tener acceso a los archivos de registro en instancias de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] sin conexión, se debe tener acceso de lectura tanto al espacio de nombres WMI **Root\Microsoft\SqlServer\ComputerManagement10** como a la carpeta donde están almacenados los archivos de registro. Para obtener más información, vea la sección Seguridad del tema [Ver archivos del registro sin conexión](view-offline-log-files.md).  
  
## <a name="see-also"></a>Vea también  
 [Visor de archivos de registro](log-file-viewer.md)   
 [Abrir el Visor de archivos de registro](open-log-file-viewer.md)   
 [Ver archivos del registro sin conexión](view-offline-log-files.md)  
  
  
