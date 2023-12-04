# POSICIONAMIENTO
import machine
import utime

# Configura los pines para el control del motor paso a paso
motor_in1 = machine.Pin(5, machine.Pin.OUT)
motor_in2 = machine.Pin(4, machine.Pin.OUT)
motor_in3 = machine.Pin(0, machine.Pin.OUT)
motor_in4 = machine.Pin(2, machine.Pin.OUT)

# Configura la secuencia de pasos para un motor paso a paso bipolar (ajusta según tu motor)
sequence = [(1, 0, 0, 1), (0, 1, 0, 1), (0, 1, 1, 0), (1, 0, 1, 0)]

# Configura la velocidad del motor (ajusta según sea necesario)
delay = 0.001  # Puedes ajustar este valor para cambiar la velocidad

# Calcula la cantidad de pasos necesarios para girar un giro completo (360 grados)
pasos_giro_completo = 24

# Habilita el motor
motor_enabled = True

while True:
    # Gira en sentido antihorario durante un giro completo (180 grados)
    for _ in range(pasos_giro_completo):
        if motor_enabled:
            for step in sequence:
                motor_in1.value(step[0])
                motor_in2.value(step[1])
                motor_in3.value(step[2])
                motor_in4.value(step[3])
                utime.sleep_us(int(delay * 1000000))

    # Detén el motor y espera 5 segundos
    motor_in1.value(0)
    motor_in2.value(0)
    motor_in3.value(0)
    motor_in4.value(0)
    utime.sleep(2)
