# Hotel guest booking analysis

How long do guests usually stay? I started with that question and found that the hardest part was deciding which bookings could answer it. In this practice dataset, 887 bookings have a checkout date earlier than check-in. Turning those differences into positive numbers would give them a plausible length without telling us how long anyone stayed.

I used Python, pandas and Plotly to explore 2,000 fictional hotel bookings. Alongside stay length, I looked at common email domains and whether repeat bookings could help identify corporate accounts. This is a guided project based on a [Claude Code data analysis tutorial](https://www.youtube.com/watch?v=IPKOx66fogE).

## What I found

| Question | Result from the 2,000-booking file |
| --- | --- |
| How long was a typical stay? | The median was **15 nights** and the mean was **18.7 nights** across 1,044 usable bookings, including 31 same-day stays. |
| How complete were the dates? | 887 bookings had checkout before check-in and 69 had no checkout date. Together they account for **47.8%** of the file, so the median describes only the usable bookings. |
| Which email domains appeared most often? | Gmail appeared on 771 bookings (38.6%), Outlook on 409 (20.5%) and Yahoo on 252 (12.6%). Each booking counts once. |
| Could I identify corporate accounts? | All 2,000 billing addresses were unique after standardising spacing and case. Four email addresses appeared twice. No address reached the notebook’s five-booking threshold, and the file has no customer-type field to confirm who booked for work. |

The difference between a booking and a customer matters here. Two bookings with the same email are a reason to look closer. A shared email provider alone tells us very little about whether two guests belong to the same company.

## Explore the project

- [Hotel guest exploration](hotel_guests_exploration.ipynb) contains the data checks, charts and booking export. Its default input is the 2,000-row file. Some written notes in the notebook refer to an earlier 100-row sample. The figures above were calculated from the current full file.
- [Booking-level export](output/bookings_clean.csv) contains derived fields such as stay length, date status and repeat-booking counts. It keeps rows with date problems so they can be inspected.
- [Synthetic data notebook](create_synthetic_data.ipynb) shows how the tutorial uses SDV to generate a smaller practice dataset. The [data folder](data/) contains the fictional source, the 100-row synthetic sample and the SDV metadata.

## Run the analysis

From the project folder on macOS or Linux, run:

```bash
python3 -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
python -m jupyter lab
```

Open `hotel_guests_exploration.ipynb` and run the cells in order. The final cell writes `output/bookings_clean.csv`. To explore the smaller sample, change `DATA_PATH` to `data/hotel_guests_data_synthetic.csv` before running the notebook. That run replaces the export with results for the selected input. The synthetic sample is already included, so generating it again is optional.
