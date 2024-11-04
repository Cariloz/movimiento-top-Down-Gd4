# movimiento-top-Down-Gd4

extends CharacterBody2D

#modifica la velocidad del personaje a tu gusta weon 
const SPEEDING = 180

#esto no es necesario pero si quieres hacer una forma mas rápida para llamar al sprite y colisión añadelo
@onready var BILL = $BILLY
@onready var COLI = $COLISI


#añade tus funciones brother 
func _physics_process(_delta):
	movimiento()
	direccion()
	Animated()

func Animated():
	#esta parte es muy compleja pero resumidamente lo único que hace es asignar la tecla y reproducir la animación 
	var velocity = Vector2.ZERO
	if Input.is_action_pressed("ui_up"):
		velocity.y -= 1
		BILL.play("runUp")
	elif Input.is_action_pressed("ui_down"):
		velocity.y += 1
		BILL.play("runDown")
	elif Input.is_action_pressed("ui_right"):
		velocity.x += 1
		BILL.play("run")
	elif Input.is_action_pressed("ui_left"):
		velocity.x -= 1
		BILL.play("run")
	else:
		BILL.play("idle")
		velocity = velocity.normalized() * SPEEDING

func movimiento():
	#asigna las teclas con las que se mueve el personaje brothers
	velocity = Input.get_vector("ui_left", "ui_right", "ui_up", "ui_down") * SPEEDING
	velocity.normalized()
	move_and_slide()
	

func direccion():
	#rota el Sprite con un flip, o sea la dirección de billy
	if velocity.x > 0:
		BILL.flip_h = false
	elif velocity.x < 0:
		BILL.flip_h = true
  
