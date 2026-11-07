# 6.1GDV
# Mini-level — Inleveren

**Naam:**  Min   
**Klas:**  SD1A 
**Datum:**  11/7/2026   
**Les:** GDV Les 6

---

## Wat heb ik gemaakt?

Ik heb een 2.5d level gemaakt waarin je 5 munten moet oppakken om een sleutel te krijgen, dan kan je een deur openmaken en zo is die klaar.

...

---

## Screenshot / GIF van je level

[6.1GDV](https://drive.google.com/file/d/1vwbmAOVSM5rqGWzVr9w8gds_wce6s144/view?usp=sharing)
(Vid was too long to be a gif :sob:)

---

## Bewegend object

2 objecten bewegen, de player (die beweegt med WASD en SPACE.) en munten die rond draieen.

...

```csharp

# Player movement


    void Update()
    {
       

        if (Input.GetKeyDown(KeyCode.Space) && stamina > 0)
        {
            jump();
        }

        Movement();

    }
    void Movement()
    {
        Vector3 moveX = Vector3.left * speed * Input.GetAxis("Horizontal") * Time.deltaTime;
        transform.position += moveX;

        Vector3 moveZ = Vector3.back * speed * Input.GetAxis("Vertical") * Time.deltaTime;
        transform.position += moveZ;
    }

    void jump()
    {
        rb.AddForce(Vector3.up * jumpforce);
        stamina--;

    }
  



# SpinOBJ

    public float rotateSpeed = 90f;

    void Update()
    {
        transform.Rotate(0,0, rotateSpeed * Time.deltaTime);
    }




```

---

## Collider of trigger

De objecten met triggers zijn, De deur, Npc en muntjes

...

```csharp
# Door
    private void OnTriggerEnter(Collider other)
    {
        if (other.CompareTag("Player"))
        {
            playerNear = true;
            Debug.Log("Press E to open");
        }
    }

    private void OnTriggerExit(Collider other)
    {
        if (other.CompareTag("Player"))
        {
            playerNear = false;
        }
    }

#NPC
    private void OnTriggerEnter(Collider other)
    {
        if (other.CompareTag("Player"))
        {
            playerNearby = true;
            Debug.Log("Press E to talk");
        }
    }

    private void OnTriggerExit(Collider other)
    {
        if (other.CompareTag("Player"))
        {
            playerNearby = false;
        }
    }

#Coins
    private void OnTriggerEnter(Collider other)
    {
        if (other.CompareTag("Player"))
        {
         
            amountCoins++;

            Debug.Log($"Coins collected = {amountCoins}");

            if (amountCoins == coinsNeeded)
            {
                Debug.Log("Go talk to XXX");
            }

            Destroy(gameObject);
        }
    }

```

---

## Logica met `if` of `switch`

als de player een sleutel heeft dan opent een deur

...

```csharp
 if (playerNear && Input.GetKeyDown(KeyCode.E))
 {
     if (HasKey.hasKey)
     {
         Debug.Log("Door opened!");

         closedDoor.SetActive(false);
         
     }
     else
     {
         Debug.Log("Need a key!");
     }
 }

```

---

## Eigen extra idee

ik had een soort NPC gemaakt, die een bepaalde hoeveelheid munten vraagt. als je die pakt dan krijg je pas een sleutel.

...

```csharp
public class TalkingToNPC : MonoBehaviour
{
    private bool playerNearby = false;

    private void Update()
    {
        if (playerNearby && Input.GetKeyDown(KeyCode.E))
        {
            Talk();
        }
    }

    void Talk()
    {
        if (DestroyOnTrigger.amountCoins >= DestroyOnTrigger.coinsNeeded)
        {
            Debug.Log("Thanks. Here's that key.");
            Debug.Log("* You received a key! *");

            HasKey.hasKey = true;
        }
        else
        {
            Debug.Log("If you can find me 5 coins, I'll give you a key.");
        }
    }

    private void OnTriggerEnter(Collider other)
    {
        if (other.CompareTag("Player"))
        {
            playerNearby = true;
            Debug.Log("Press E to talk");
        }
    }

    private void OnTriggerExit(Collider other)
    {
        if (other.CompareTag("Player"))
        {
            playerNearby = false;
        }
    }
}
```

---

## Evaluatie

### Wat ging goed? en waarom?

De graphics, ik vind de 2.5 stijl prachtig- though ik had geen tijd om de anti aliasing te fixen..

...

### Wat vond je lastig? en waarom?

om andere scripts en datatypen in een nieuwe script te referencen.

...

### Wat zou je een volgende keer anders doen?

om betere namen te geven aan mijn strings en ints :sob: ik vond het confusing om alles te herinneren tbh

...
