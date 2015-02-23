package kodut55;

import java.util.Random;
import java.util.Scanner;

public class Kakskend1 {
	
	// Kirjutada meetod, mis võtab ette kolm arvu (eraldi argumentidena) ja tagastab neist suurima.

	private static Scanner scanner = new Scanner(System.in);
	Scanner keyboard = new Scanner(System.in);

	public static void main(String[] args) {
		new Kakskend1().run();
	}

	public void run() {

		int raha;
		int panus;
		boolean kasutajav5it;

		System.out.println("Tere tulemast mängu BlackJack");
		System.out.println();

		raha = 100; // alguses on 100 ühikut raha

		while (true) {
			System.out.println("Sul on " + raha + " eurot.");
			do {

				System.out
						.println("Mitu eurot tahad panustada (Vajuta 0, et katkestada)");

				panus = keyboard.nextInt();
				if (panus < 0 || panus > raha) {
					System.out.println("Sinu panus peab jääma vahemikku 0 ja "
							+ raha + ".");
				}
			} while (panus < 0 || panus > raha);
			if (panus == 0) {
				raha = raha + panus;
				break;
			}
			kasutajav5it = Blackjack();
			if (kasutajav5it) {
				raha = raha + panus;
			} else {
				raha = raha - panus;
			}
			System.out.println();
			if (raha == 0) {
				System.out.println("Sinu rahakott on tühi!");
				break;
			}
		}

		System.out.println();
		System.out.println("Lahkud mängust " + raha + " euroga.");
	}

	private boolean Blackjack() {

		Scanner keyboard = new Scanner(System.in);

		int[] uusKaart = { 2, 2, 2, 2, 3, 3, 3, 3, 4, 4, 4, 4, 5, 5, 5, 5, 6,
				6, 6, 6, 7, 7, 7, 7, 8, 8, 8, 8, 9, 9, 9, 9, 10, 10, 10, 10,
				10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 11, 11, 11, 11 };

		shuffleArray(uusKaart);

		System.out.println();
		System.out.println("Sinu kaardid on: " + uusKaart[0] + " ja "
				+ uusKaart[1] + ".");
		int mKogusumma = uusKaart[0] + uusKaart[1];
		System.out.println("Sinu kogusumma on: " + mKogusumma + ".");
		System.out.println();

		// kui esimeses roundis blackjack
		if (mKogusumma == 21) {
			System.out.println("BLACKJACK, sinu võit!");
			return true;
		}
		if (mKogusumma > 21) {
			System.out.println("Lõhki, kaotasid!");
			return false;
		}
		// Dealer cards
		System.out.println("Diileril on: " + uusKaart[2]
				+ " ja varjatud kaardid");
		int dKogusumma = uusKaart[2] + uusKaart[3];
		if (dKogusumma > 21) {
			System.out.println();
			System.out.println("Diileri kogusumma on: " + dKogusumma + ".");
			System.out.println("Diiler läks lõhki, sinu võit!");
			return true;
		}
		if (dKogusumma == 21) {
			System.out.println();
			System.out.println("Diiler paljastab oma teise kaardi: "
					+ uusKaart[3] + ".");
			System.out.println("Diileri kogusumma on: " + dKogusumma + ".");
			System.out.println();
			System.out.println("Diileril on BLACKJACK, kaotasid!");
			return false;
		}
		System.out.println("Tema kogusumma on peidetud!");
		System.out.println();

		// juurde või stopp

		System.out.print("Tahad kaarte \"juurde\" või \"l6pp\"? ");
		String hitStay = keyboard.next();
		System.out.println();

		// cc = kaartide arv
		int cc = 4;
		if (hitStay.equalsIgnoreCase("juurde")) {

			while (mKogusumma < 21 && hitStay.equalsIgnoreCase("juurde")) {
				if (hitStay.equalsIgnoreCase("juurde")) {
					System.out.println("Sa tõmbasid: " + uusKaart[cc] + ".");
					mKogusumma = mKogusumma + uusKaart[cc];
					System.out
							.println("Sinu kogusumma on: " + mKogusumma + ".");
					System.out.println();
					cc++;

					if (mKogusumma > 21) {
						System.out.println("Läksid lõhki, kaotasid!");
						return false;
					}
					if (mKogusumma == 21) {
						System.out.println("BLACKJACK, sinu võit!");
						return true;
					}
					System.out.print("Tahad kaarte \"juurde\" või \"l6pp\"? ");
					hitStay = keyboard.next();
					System.out.println();

					
					if (hitStay.equalsIgnoreCase("l6pp")) {

						while (mKogusumma < 21
								&& hitStay.equalsIgnoreCase("l6pp")) {
							if (hitStay.equalsIgnoreCase("l6pp")) {
								System.out
										.println("Sa ei võtnud kaarte juurde");

								System.out.println("Sinu kogusumma on: "
										+ mKogusumma + ".");
								System.out.println("Diileri kogusumma on: "
										+ dKogusumma + ".");
								System.out.println();
								cc++;

								if (mKogusumma > 21) {
									System.out
											.println("Läksid lõhki, kaotasid!");
									return false;
								}
								if (mKogusumma == 21) {
									System.out.println("BLACKJACK, sinu võit!");
									return true;
								}
								if (mKogusumma == dKogusumma) {
									System.out.println("VIIK");
									return true;

								}
								if (mKogusumma < 21 && mKogusumma > dKogusumma) {
									System.out.println("SINU VÕIT");
									return true;

								}
								if (mKogusumma < 21 && mKogusumma < dKogusumma) {
									System.out.println("KAOTASID");
									return false;

								}
							}

						}

						keyboard.close();
						System.out.println("Diileri kord");
						System.out.println("Tema peidetud kaart on: "
								+ uusKaart[3] + ".");

						cc++;
						while (dKogusumma < 16) {
							System.out.println();
							System.out.println("Diiler võtab juurde.");
							System.out.println("Ta tõmbab: " + uusKaart[cc]
									+ ".");
							cc++;
							dKogusumma = dKogusumma + uusKaart[cc];
							System.out.println();
							System.out.println("Tema kogusumma on: "
									+ dKogusumma);

							if (dKogusumma > 21) {
								System.out.println();
								System.out
										.println("Diiler läks lõhki, sinu võit!");
								return true;
							}

							if (dKogusumma < 21 && dKogusumma > 16) {
								System.out.println();
								System.out.println("Diiler passib.");
							}
						}

						// Lõplik kokkuvõte
						System.out.println();
						System.out.println("Diileri kogusumma on: "
								+ dKogusumma);
						System.out.println("Sinu kogusumma on: " + mKogusumma);
						System.out.println();

						if (dKogusumma > mKogusumma) {
							System.out.println("Diiler võitis!");
						}
						if (dKogusumma == mKogusumma) {
							System.out.println("Viik!");

						}
						if (dKogusumma < mKogusumma) {
							System.out.println("Sinu võit!");

						}
					}
				}
			}
		}
		return false;
	}

	static void shuffleArray(int[] deckCards) {

		Random rnd = new Random();
		for (int i = deckCards.length - 1; i > 0; i--) {
			int index = rnd.nextInt(i + 1);
			// vahetus
			int a = deckCards[index];
			deckCards[index] = deckCards[i];
			deckCards[i] = a;
		}
	}
}
