using UnityEngine;

public class PlayerController : MonoBehaviour
{
    [Header("Movement")]
    public float moveSpeed = 5f;
    public float jumpForce = 7f;

    [Header("Mobile Joystick")]
    public Joystick joystick;

    private Rigidbody rb;
    private bool grounded;

    void Start()
    {
        rb = GetComponent<Rigidbody>();
    }

    void Update()
    {
        // PC Controls
        float keyboardX = Input.GetAxis("Horizontal");
        float keyboardZ = Input.GetAxis("Vertical");

        // Mobile Controls
        float mobileX = 0f;
        float mobileZ = 0f;

        if (joystick != null)
        {
            mobileX = joystick.Horizontal;
            mobileZ = joystick.Vertical;
        }

        // Use whichever input is being used
        float x = Mathf.Abs(mobileX) > 0.1f ? mobileX : keyboardX;
        float z = Mathf.Abs(mobileZ) > 0.1f ? mobileZ : keyboardZ;

        Vector3 direction = new Vector3(x, 0, z);

        // Move
        if (direction.magnitude > 0.1f)
        {
            transform.Translate(
                direction.normalized * moveSpeed * Time.deltaTime,
                Space.World
            );
        }

        // PC Jump
        if (Input.GetKeyDown(KeyCode.Space) && grounded)
        {
            Jump();
        }
    }

    public void Jump()
    {
        if (grounded)
        {
            rb.AddForce(Vector3.up * jumpForce, ForceMode.Impulse);
            grounded = false;
        }
    }

    private void OnCollisionEnter(Collision collision)
    {
        if (collision.gameObject.CompareTag("Ground"))
        {
            grounded = true;
        }
    }
}
