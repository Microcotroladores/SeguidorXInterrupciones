;-----------encabezado
            #INCLUDE<P16F84A.INC>
            __CONFIG    _XT_OSC & _PWRTE_ON
;----------definiciones
            #DEFINE SD2 PORTB,4
            #DEFINE SD1 PORTB,5
            #DEFINE SI1 PORTB,6
            #DEFINE SI2 PORTB,7
;----------o    o  |   |  o    o-----------
;---------si2  si1 |   | sd1   sd2-------
;----------registros
            CBLOCK  0CH
            V1
            V2
            V3
            ENDC
;-----------configuración
            ORG     00H
            GOTO    INICIO

            ORG     04H
            GOTO    KAOS
;-----------CONFIGURACIÓN DEL PIC
INICIO:     BSF     STATUS,RP0
            BSF     INTCON,GIE
            BSF     INTCON,RBIE
            MOVLW   0F0H
            MOVWF   TRISB
            CLRF    TRISA
            BCF     STATUS,RP0
            CLRF    PORTA
            CLRF    PORTB
            GOTO    RUN         ;ADELANTE
;-----------INTERRUPCIÓN REALIZADA
KAOS:       BTFSC   SD2
            GOTO    DER
            CALL    ABI
            BTFSC   SD1
            GOTO    DER
            CALL    ABI
            BTFSC   SI1
            GOTO    IZQ
            CALL    ABI
            BTFSC   SI2
            GOTO    IZQ
            CALL    ABI
;-----------HABILITACIÓN
ABI:        BSF     INTCON,GIE
            BCF     INTCON,RBIF
            RETURN
;-----------MOVIMIENTOS
RUN:        MOVLW   b'00000101'
        	MOVWF   PORTA
            GOTO    $-1

DER:        MOVLW   b'00000110'
            MOVWF   PORTA
            CALL    PAUSA
            MOVLW   00H
            MOVWF   PORTA
            CALL    PAUSA
            CALL    ABI		;ajustar dependiendo de pruebas
            RETFIE

IZQ:        MOVLW   b'00001001'
            MOVWF   PORTA
            CALL    PAUSA
            MOVLW   10H
            MOVWF   PORTA
            CALL    PAUSA
            CALL    ABI
            RETFIE

REV:        MOVLW   b'00001010'
            MOVWF   PORTA
            CALL    PAUSA
            MOVLW   10H
            MOVWF   PORTA
            CALL    PAUSA
            CALL    ABI
			RETFIE
;-----------TIEMPOS
PAUSA:      MOVLW   .1
            MOVWF   V1
            MOVLW   .40
            MOVWF   V2
            MOVLW   .40
            MOVWF   V3
            DECFSZ  V3,F
            GOTO    $-1
            DECFSZ  V2,F
            GOTO    $-5
            DECFSZ  V1,F
            GOTO    $-9
            RETURN
;-----------FIN
            END
