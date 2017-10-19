# Addicto

GAME MANAGER:

using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.UI;

public class mouse_drag_drop : MonoBehaviour {


	public Game_manager gm;

	public Text questions;
	public Vector2 big_truck_ip;
	public Vector2 small_truck_ip;

	public Vector2 correct_ip;
	public Vector2 incorrect_ip;




	public Vector2 mouseposition;
//	public Text score_text;
//	public int score;
	public GameObject small_truck;
	public GameObject big_truck;

	public GameObject true1;
	public GameObject false1;

	public static int i;
	public static int result;
	public bool move_truck;
	// Use this for initialization
	void Start () {
		move_truck = true;
		big_truck_ip = new Vector2 (big_truck.transform.position.x, big_truck.transform.position.y);
		small_truck_ip = new Vector2 (small_truck.transform.position.x, small_truck.transform.position.y);
		correct_ip =  new Vector2(true1.transform.position.x, true1.transform.position.y);
		incorrect_ip = new Vector2 (false1.transform.position.x, false1.transform.position.y);

		i = 1;
		result = 1;
	}
	
	// Update is called once per frame
	void Update () {
		if (big_truck.transform.position.x >= -4.5f && move_truck ==true) {
			correct_ip =  new Vector2(true1.transform.position.x, true1.transform.position.y);
			incorrect_ip = new Vector2 (false1.transform.position.x, false1.transform.position.y);
			move_truck = false;
		}


	}

	public void OnMouseDrag()
	{
		if (move_truck == false) {
			//Debug.Log ("hello");
			mouseposition = Input.mousePosition;
			mouseposition = Camera.main.ScreenToWorldPoint (mouseposition);
			gameObject.transform.position = new Vector2 (mouseposition.x, mouseposition.y);
		}

	}



	public void OnTriggerEnter2D(Collider2D other) 
	{
		if (other.gameObject.tag == "Player") {
			Debug.Log ("hello");


			//Debug.Log (gameObject.transform.name);
			if (gameObject.transform.name == "true" && (i == 1 || i == 2 || i == 4 || i == 7 || i == 9 || i == 10)) {
				//gameObject.SetActive (false);
//				score += 10;
//				score_text.text = "Score: " + score.ToString ();
				gm.audiosource.clip = gm.audioclip[0];
				gm.audiosource.Play ();
				gm.score_add();

				StartCoroutine (nextquestion (1.0f));
			} else if ((gameObject.transform.name == "false" || gameObject.transform.name == "falsee") && (i == 3 || i == 5 || i == 6 || i == 8)) {
//				score += 10;
//				score_text.text = "Score: " + score.ToString ();
				gm.audiosource.clip = gm.audioclip[0];
				gm.audiosource.Play ();
				gm.score_add();
				StartCoroutine (nextquestion (1.0f));
			} else {
				gm.audiosource.clip = gm.audioclip[1];
				gm.audiosource.Play ();
				gm.score_minus ();

//				score -= 10;
//	            score_text.text = "Score: " + score.ToString ();
				StartCoroutine (nextquestion (1.0f));
			}
		}

	}

	IEnumerator nextquestion(float timel)
	{
		yield return new WaitForSeconds (timel);
		i++;
		Debug.Log (i);
		//big_truck.transform.Translate (-14.3f,big_truck.transform.position.y,big_truck.transform.position.z);
		//small_truck.transform.Translate (12.33f, small_truck.transform.position.y, small_truck.transform.position.z);
//		big_truck.transform.position = big_truck_ip;
//		small_truck.transform.position = small_truck_ip;
//




		true1.transform.position = correct_ip;
		false1.transform.position = incorrect_ip;

		Game_manager.big_transforms = true;
		Game_manager.small_transforms = true;
		questions.text = " ".ToString ();
	}

}

