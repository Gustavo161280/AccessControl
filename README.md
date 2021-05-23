# AccessControl
Es un pequeño programa creado en java
package AccessControl;

import java.io.*;
import javax.swing.*;
import java.awt.*;
import java.util.*;
import javax.swing.plaf.*;

/**
 *
 * @author Gustavo Señorans
 */
public class AccessControl {

    /**
     * ---------------- + VARIABLES -----------------
     */
    sos sos = new sos();
    UIManager UI = new UIManager();
    salida salida = new salida();
    entrada entrada = new entrada();
    explosimetro_salida explosimetro_salida = new explosimetro_salida();
    explosimetro_entrada explosimetro_entrada = new explosimetro_entrada();
    walkie_salida walkie_salida = new walkie_salida();
    walkie_entrada walkie_entrada = new walkie_entrada();
    menu_ropa menu_ropa = new menu_ropa();
    menu_llaves menu_llaves = new menu_llaves();
    modificaciones modificaciones = new modificaciones();
    modificacion_paqueteria modificacion_paqueteria = new modificacion_paqueteria();
    modificacion_material modificacion_material = new modificacion_material();
    moficicacion_lista_material moficicacion_lista_material = new moficicacion_lista_material();
    lista_material lista_material = new lista_material();
    copias copias = new copias();
    copias_control_acceso copias_control_acceso = new copias_control_acceso();
    menu_telf menu_telf = new menu_telf();
    recepcion recepcion = new recepcion();
    envio envio = new envio();
    date date = new date();
    alta alta = new alta();

    //DATO BOOLEANO PARA CERRAR PROGRAMA
    boolean valor = false;
    String user = System.getProperty("user.name");
    //VARIABLE PARA ICONO DEL PANEL DE CONTROL
    ImageIcon icono2 = new ImageIcon("S:\\llauversema_logo.jpg");

    //VARIABLE PARA FICHEROS
    File emergencia = new File("S:\\emergencia.csv");
    File fichero = new File("S:\\entrada.csv");
    File bd = new File("S:\\bd.csv");
    File bd_card_null = new File("S:\bdSinTarjeta.csv");

    public static void main(String[] args) {

        AccessControl programa = new AccessControl();
        programa.inicio();
    }

    /**
     * ---------------- PÁGINA PRINCIPAL -----------------
     *
     * @param f
     */
    public static void setUIFont(FontUIResource f) {
        Enumeration keys = UIManager.getDefaults().keys();
        while (keys.hasMoreElements()) {
            Object key = keys.nextElement();
            Object value = UIManager.get(key);
            if (value instanceof FontUIResource) {
                FontUIResource orig = (FontUIResource) value;
                Font font = new Font(f.getFontName(), orig.getStyle(), f.getSize());
                UIManager.put(key, new FontUIResource(font));
            }
        }
    }

    private void inicio() {
        File directorio = new File("C:\\Users\\" + user + "\\Desktop\\Ficheros");
        if (!directorio.exists()) {
            directorio.mkdirs();
        }
        //COLORES PARA PANEL DE CONTROL
        UIManager.put("OptionPane.minimumSize", new Dimension(550, 250));
        UIManager.put("OptionPane.background", new Color(204, 102, 0));
        UIManager.put("Panel.background", new Color(255, 255, 255));
        UIManager.put("Button.foreground", new Color(0, 0, 0));
        UIManager.put("OptionPane.messageForeground", new Color(0, 0, 0));
        UIManager.put("OptionPane.font", new Color(0, 0, 0));
        UIManager.put("OptionPane.okButtonText", "Aceptar");
        UIManager.put("OptionPane.cancelButtonText", "Cancelar");
        setUIFont(new FontUIResource(new Font("Calibri", 0, 22)));
        JPanel p = new JPanel();
        copias.copias2();
        copias_control_acceso.copias2();

        //DATOS PARA MENU 
        while (!valor) {
            Object[] menu = {"ENTRADA", "ENTRADA NOMBRE/APELLIDO", "SALIDA", "SALIDA NOMBRE/APELLIDO", "CREAR BD",
                "HORARIOS", "EMERGENCIAS", "PAQUETERÍA", "MATERIAL", "ROPA", "LLAVES", "TELÉFONO", "CERRAR"};
            Object[] menu2 = {"ENTRADA", "SALIDA", "MODIFICACIONES", "MENU PRINCIPAL"};
            Object[] menu3 = {"PERSONAS EN PLANTA", "CREAR FICHERO CON DATOS DE LAS PERSONAS DENTRO DE PLANTA",
                "NÚM. TELF. EMERGENCIA PLAN DE AUTOPROTECCIÓN", "NÚM. TELF. EMERGENCIA ACTIVACIÓN DEL PIM",
                "NÚM. TELF. EMERGENCIA PLAN INTERIOR MARÍTIMO DE VERTIDO AL MAR", "MENU PRINCIPAL"};
            Object[] menu4 = {"LISTADO MATERIAL", "RECEPCIÓN", "ENVIO", "MODIFICACIONES", "MENU PRINCIPAL"};
            Object[] menu5 = {"EXPLOSIMETRO", "WALKIE", "MODIFICACIONES", "MENU PRINCIPAL"};
            Object[] menu6 = {"SALIDA", "ENTRADA", "MENU PRINCIPAL"};
            Object[] menu7 = {"NUEVO MATERIAL", "MODIFICACIONES", "MENU PRINCIPAL"};
            Object[] menu8 = {"MODIFICAR PRODUCTO", "MODIFICAR PROVEEDOR", "MODIFICAR PRESENTACIÓN", "MODIFICAR ALMACENAJE", "MODIFICAR NOMBRE COMERCIAL",
                "MODIFICAR DEPARTAMENTO", "MENU PRINCIPAL"};
            String opcion = (String) JOptionPane.showInputDialog(null, ""
                    + date.fecha() + "\nMENU PRINCIPAL", "LLAUVERSEMA", 0, icono2, menu, menu[0]);

            switch (opcion) {
                case "ENTRADA":
                    entrada.entrada_rapida_planta();
                    break;
                case "ENTRADA NOMBRE/APELLIDO":
                    entrada.entrada_planta_por_nombre();
                    break;
                case "SALIDA":
                    salida.salida_rapida_card();
                    break;
                case "SALIDA NOMBRE/APELLIDO":
                    salida.nombre_apellido();
                    break;
                case "CREAR BD":
                    alta.menu_alta();
                    break;
                case "HORARIOS":
                    String opcion2 = (String) JOptionPane.showInputDialog(null, ""
                            + date.fecha() + "\nHORARIOS",
                            "LLAUVERSEMA", 0, icono2, menu2, menu2[0]);
                    switch (opcion2) {
                        case "ENTRADA":
                            entrada.menu_entrada_planta();
                            break;
                        case "SALIDA":
                            salida.menu_salida_planta();
                            break;
                        case "MODIFICACIONES":
                            modificaciones.menu_modific();
                            break;
                        case "MENU PRINCIPAL":
                    }
                    break;
                case "EMERGENCIAS":
                    String opcion3 = (String) JOptionPane.showInputDialog(null, ""
                            + date.fecha() + "\nEMERGENCIAS", "LLAUVERSEMA", 0, icono2, menu3, menu3[0]);
                    switch (opcion3) {
                        case "PERSONAS EN PLANTA":
                            sos.emergencia();
                            break;
                        case "CREAR FICHERO CON DATOS DE LAS PERSONAS DENTRO DE PLANTA":
                            sos.emergencia();
                            sos.file_sos();
                            break;
                        case "NÚM. TELF. EMERGENCIA PLAN DE AUTOPROTECCIÓN":
                            JOptionPane.showMessageDialog(null, date.fecha() + "\n\nNÚMERO DE TELÉFONO DE EMERGECIA\nPARA EL "
                                    + "PLAN DE AUTOPROTECCIÓN ES:  \n[ BOMBEROS: 080\nCENTRO CONTROL POLICIA PORTUARIA: 900 100 852"
                                    + "\nEMERGENCIAS: 112\nCECAT: ??? ??? ???\nLLAUVERSEMA: ??? ??? ??? ]\n\n",
                                    "LLAUVERSEMA", JOptionPane.QUESTION_MESSAGE, icono2);
                            break;
                        case "NÚM. TELF. EMERGENCIA ACTIVACIÓN DEL PIM":
                            JOptionPane.showMessageDialog(null, date.fecha() + "\n\nNÚMERO DE TELÉFONO DE EMERGECIA\nPARA LA"
                                    + " ACTIVACIÓN DEL PIM ES:  \n[ CCS BCN: ??? ??? ???\n CECOPORT: ??? ??? ??? ]\n\n",
                                    "LLAUVERSEMA", JOptionPane.QUESTION_MESSAGE, icono2);
                            break;
                        case "NÚM. TELF. EMERGENCIA PLAN INTERIOR MARÍTIMO DE VERTIDO AL MAR":
                            JOptionPane.showMessageDialog(null, date.fecha() + "\n\nNÚMERO DE TELÉFONO DE EMERGECIA PARA EL\nPLAN INTERIOR MARÍTIMO DE"
                                    + " VERTIDO AL MAR ES:  \n[ MOORING: ??? ??? ???\n ??? ??? ??? ]\n\n",
                                    "LLAUVERSEMA", JOptionPane.QUESTION_MESSAGE, icono2);
                            break;
                        case "MENU PRINCIPAL":
                    }
                    break;
                case "PAQUETERÍA":
                    String opcion4 = (String) JOptionPane.showInputDialog(null, ""
                            + date.fecha() + "\nPAQUETERIA", "LLAUVERSEMA", 0, icono2, menu4, menu4[0]);
                    switch (opcion4) {
                        case "LISTADO MATERIAL":
                            String opcion8 = (String) JOptionPane.showInputDialog(null, ""
                                    + date.fecha() + "\nLISTADO MATERIAL", "LLAUVERSEMA", 0, icono2, menu7, menu7[0]);
                            switch (opcion8) {
                                case "NUEVO MATERIAL":
                                    lista_material.nuevo_material();
                                    break;
                                case "MODIFICACIONES":
                                    String opcion7 = (String) JOptionPane.showInputDialog(null, ""
                                            + date.fecha() + "\nLISTADO MATERIAL", "LLAUVERSEMA", 0, icono2, menu8, menu8[0]);
                                    switch (opcion7) {
                                        case "MODIFICAR PRODUCTO":
                                            moficicacion_lista_material.modificar_producto();
                                            break;
                                        case "MODIFICAR PROVEEDOR":
                                            moficicacion_lista_material.modificar_proveedor();
                                            break;
                                        case "MODIFICAR PRESENTACIÓN":
                                            moficicacion_lista_material.modificar_presentacion();
                                            break;
                                        case "MODIFICAR ALMACENAJE":
                                            moficicacion_lista_material.modificar_almacenaje();
                                            break;
                                        case "MODIFICAR NOMBRE COMERCIAL":
                                            moficicacion_lista_material.modificar_nombreComercial();
                                            break;
                                        case "MODIFICAR DEPARTAMENTO":
                                            moficicacion_lista_material.modificar_departamento();
                                            break;
                                        case "MENU PRINCIPAL":
                                    }
                                    break;
                                case "MENU PRINCIPAL":
                            }
                            break;
                        case "RECEPCIÓN":
                            recepcion.recepcion();
                            break;
                        case "ENVIO":
                            envio.envio();
                            break;
                        case "MODIFICACIONES":
                            modificacion_paqueteria.menu_modificacion();
                            break;
                        case "MENU PRINCIPAL":
                    }
                    break;
                case "MATERIAL":
                    String opcion5 = (String) JOptionPane.showInputDialog(null, ""
                            + date.fecha() + "\nEXPLOSIMETROS Y WALKIES", "LLAUVERSEMA", 0, icono2, menu5, menu5[0]);
                    switch (opcion5) {
                        case "EXPLOSIMETRO":
                            String opcion9 = (String) JOptionPane.showInputDialog(null, ""
                                    + date.fecha() + "\nEXPLOSIMETROS", "LLAUVERSEMA", 0, icono2, menu6, menu6[0]);
                            switch (opcion9) {
                                case "SALIDA":
                                    explosimetro_salida.salida_explosimetro();
                                    break;
                                case "ENTRADA":
                                    explosimetro_entrada.entrada_explosimetro();
                                    break;
                                case "MENU PRINCIPAL":
                            }
                            break;
                        case "WALKIE":
                            String opcion6 = (String) JOptionPane.showInputDialog(null, ""
                                    + date.fecha() + "\nWALKIE", "LLAUVERSEMA", 0, icono2, menu6, menu6[0]);
                            switch (opcion6) {
                                case "SALIDA":
                                    walkie_salida.salida_walkie();
                                    break;
                                case "ENTRADA":
                                    walkie_entrada.entrada_walkie();
                                    break;
                                case "MENU PRINCIPAL":
                            }
                            break;
                        case "MODIFICACIONES":
                            modificacion_material.menu_modificacion_material();
                            break;
                        case "MENU PRINCIPAL":
                    }
                    break;

                case "ROPA":
                    menu_ropa.menu_stock_ropa();
                    break;
                case "LLAVES":
                    menu_llaves.menu_llaves2();
                    break;
                case "TELÉFONO":
                    menu_telf.menu_telf2();
                    break;
                case "CERRAR":
                    copias.copias2();
                    copias_control_acceso.copias2();
                    valor = true;
                    break;
            }

        }
    }
}
