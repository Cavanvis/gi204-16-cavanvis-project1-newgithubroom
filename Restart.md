using UnityEngine;
using UnityEngine.SceneManagement;

public class Restart : MonoBehaviour
{
        public void RestartCurrentScene()
    {
        SceneManager.LoadScene(SceneManager.GetActiveScene().name);
    }
}
