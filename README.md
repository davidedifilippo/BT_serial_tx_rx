# BT_serial_tx_rx

Il microcontrollore utilizzato in questa esecitazione è un microcontrollore a 32 bit Tensilica montato sulla board "AZDelivery ESP32 nodeMCU" 
Il uP consente connessioni Bluetooth tradizionali e Low energy.
Per inviare dati si utilizza l'applicazione [serial BlueTooth Terminal](https://play.google.com/store/apps/details?id=de.kai_morich.serial_bluetooth_terminal&gl=US)
serial BT terminal

## Programmazione 

Si include la libreria di gestione della comunicazione seriale tramite connessione radio Bluetooth
        
        #include "BluetoothSerial.h"
    
Creo un oggetto che rappresenti il modulo Hardware BT:
        
        BluetoothSerial SerialBT;
        
 ## Fase di setup
        
Imposto l'interfaccia di comunicazione seriale per il debug dell'applicazione:

        Serial.begin(9600);

Imposto l'interfaccia di comunicazione radio Bluetooth:
  
      if(!SerialBT.begin("ESP32_Ing_DiFi")){
          Serial.println("An error occurred initializing Bluetooth");
          while(1);
      }

Nel caso che l'interfaccia radio BT non funioni il programa si blocca dopo aver stampato un messaggio di errore.

Se invece l'inizializzazione dell'interfaccia BT ha avuto successo resto in ascolto di connessioni:

      Serial.println("Listening....");


## Fase di loop 

Ad ogni ciclo controllo se ci sono dati nel buffer di ricezione dell'interfaccia radio BT tramite il metodo:

      SerialBT.available()

che resituisce il numero di caratteri nel buffer di ricezione. Se ci sono caratteri eseguo una lettura:

      int c = SerialBT.read();

la lettura restituisce un intero.

Se c è '1' allora accendo il led sul pin 2, se c è '0' lo spengo. In tutti gli altri casi lampeggio 3 volte ad intervalli di 50ms.


