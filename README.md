






// /* eslint-disable react/prop-types */
// /* eslint-disable react/display-name */
// import { useEffect, useState } from "react";
// import "rsuite/dist/rsuite.min.css";
// import PlusRoundIcon from "@rsuite/icons/PlusRound";
// import MinusRoundIcon from "@rsuite/icons/MinusRound";
// import CopyIcon from "@rsuite/icons/Copy";
// import { DatePicker, Stack, Checkbox } from "rsuite";
// import PropTypes from "prop-types";
// import { forwardRef } from "react";
// import { Popover, Whisper, Button, Dropdown } from "rsuite";

// const MenuPopover = forwardRef(
//   ({ selectedWeek, onSelect, checkedDays, setCheckedDays, ...rest }, ref) => {
//     return (
//       <Popover ref={ref} {...rest} full>
//         <Dropdown.Menu>
//           {[
//             "Sunday",
//             "Monday",
//             "Tuesday",
//             "Wednesday",
//             "Thursday",
//             "Friday",
//             "Saturday",
//           ].map((day) => (
//             <Dropdown.Item
//               key={day}
//               eventKey={day}
//               onSelect={() =>
//                 setCheckedDays((prev) => ({ ...prev, [day]: !prev[day] }))
//               }
//             >
//               <Checkbox
//                 checked={checkedDays[day] || false}
//                 disabled={day === selectedWeek}
//               >
//                 {day}
//               </Checkbox>
//             </Dropdown.Item>
//           ))}
//           <Dropdown.Item eventKey="apply">
//             <div className="position-fixed bottom-0 end-0 p-3">
//             <button
//               className="btn btn-primary"
//               onClick={() =>
//                 onSelect(
//                   Object.keys(checkedDays).filter((day) => checkedDays[day])
//                 )
//               }
//                >
//               Apply
//             </button>
//             </div>

//           </Dropdown.Item>
//         </Dropdown.Menu>
//       </Popover>
//     );
//   }
// );

// const WeeklyHours = ({
//   register,
//   WeekAppend,
//   watch,
//   reset,
//   WeekRemove,
//   WeekFields,
//   errors,
//   setValue,
//   trigger,
// }) => {
//   const [selectedWeek, setSelectedWeek] = useState(null);
//   const [checkedDays, setCheckedDays] = useState({});
//   // useEffect(() => {
//   //   WeekFields.forEach((_, index) => {
//   //     register(`data.${index}.startDate`, {

//   //     });
//   //     register(`data.${index}.endDate`, );
//   //     [
//   //       "Sunday",
//   //       "Monday",
//   //       "Tuesday",
//   //       "Wednesday",
//   //       "Thursday",
//   //       "Friday",
//   //       "Saturday",
//   //     ].forEach((day) => {
//   //       register(`data.${index}.checked${day}`);
//   //     });
//   //   });
//   // }, [WeekFields, register]);

//   useEffect(() => {
//     WeekFields.forEach((_, index) => {
//       register(`data.${index}.startDate`, {
//         required: "Start time is required",
//         value: WeekFields[index]?.startDate || null, // Ensure a default value
//       });

//       register(`data.${index}.endDate`, {

//         value: WeekFields[index]?.endDate || null,
//       });

//       [
//         "Sunday",
//         "Monday",
//         "Tuesday",
//         "Wednesday",
//         "Thursday",
//         "Friday",
//         "Saturday",
//       ].forEach((day) => {
//         register(`data.${index}.checked${day}`, {
//           value: WeekFields[index]?.[`checked${day}`] || false,
//         });
//       });
//     });
//   }, [WeekFields, register]);

//   const handleToggle = (day) => {
//     const isChecked = WeekFields.some((entry) => entry[`checked${day}`]);
//     reset()
//     if (!isChecked) {
//       WeekAppend({
//         id: Date.now(),
//         startDate: null,
//         endDate: null,
//         [`checked${day}`]: true,
//       });
//     } else {
//       ("");
//     }
//   };
//   const handleCopyClick = (day) => {
//     reset()
//     setSelectedWeek(day);
//     setCheckedDays({});
//   };
//   const handleApply = (days) => {
//     console.log("Checked Days:", days);

//     const selectedFields = WeekFields.filter((entry) => entry[`checked${selectedWeek}`]);

//     if (selectedFields.length === 0) return;
//     days.forEach((day) => {
//       selectedFields.forEach((field) => {
//         WeekAppend({
//           id: Date.now(),
//           startDate: field.startDate,
//           endDate: field.endDate,
//           [`checked${day}`]: true,
//         });
//       });
//     });
//   };
//   return (
//     <div className="container mt-3 card">
//       <div className="card-body">
//         {[
//           "Sunday",
//           "Monday",
//           "Tuesday",
//           "Wednesday",
//           "Thursday",
//           "Friday",
//           "Saturday",
//         ].map((day) => (
//           <div className="p-1 row" key={day}>
//             <div className="d-flex align-items-center col-2">
//               <Checkbox
//                 checked={WeekFields.some((entry) => entry[`checked${day}`])}
//                 onChange={() => handleToggle(day)}
//               >
//                 {day}
//               </Checkbox>
//             </div>
//             <div className="col-6">
//               {WeekFields.some((entry) => entry[`checked${day}`]) ? (
//                 WeekFields.filter((entry) => entry[`checked${day}`]).map(
//                   (item, index) => (
//                     <div key={item.id} className="row mt-2">
//                       <div className="col-md-4">
//                         <label>Start time</label>
//                         <Stack
//                           direction="column"
//                           alignItems="flex-start"
//                           spacing={6}
//                         >
//                           <DatePicker
//                             format="HH:mm"
//                             editable={false}
//                             value={watch(`data.${index}.startDate`) || null}
//                             onChange={(date) => {
//                               setValue(`data.${index}.startDate`, date);
//                               trigger(`data.${index}.startDate`);
//                             }}
//                           />
//                         </Stack>
//                         {errors.data?.[index]?.startDate && (
//                           <p className="text-danger">
//                             {errors.data[index].startDate.message}
//                           </p>
//                         )}
//                       </div>
//                       <div className="col-md-4">
//                         <label>End time</label>
//                         <Stack
//                           direction="column"
//                           alignItems="flex-start"
//                           spacing={6}
//                         >
//                           <DatePicker
//                             format="HH:mm"
//                             editable={false}
//                             value={watch(`data.${index}.endDate`) || null}
//                             onChange={(date) => {
//                               setValue(`data.${index}.endDate`, date);
//                               trigger(`data.${index}.endDate`);

//                             }}
//                           />
//                         </Stack>
//                         {errors.data?.[index]?.endDate && (
//                           <p className="text-danger">
//                             {errors.data[index].endDate.message}
//                           </p>
//                         )}
//                       </div>
//                       <div className="mt-3 col-2 d-flex flex-row">
//                         <button
//                           type="button"
//                           className="me-2"
//                           onClick={() => {
//                             const removeIndex = WeekFields.findIndex((field) => field.id === item.id);
//                             if (removeIndex !== -1) {
//                               WeekRemove(removeIndex);
//                             }
//                           }}
//                         >
//                           <MinusRoundIcon style={{ fontSize: 15 }} />
//                         </button>
//                       </div>
//                     </div>
//                   )
//                 )
//               ) : (
//                 <p className="pt-3">Unavailable</p>
//               )}
//             </div>
//             <div className="col-2 mt-3 d-flex flex-row">
//               <button
//                 type="button"
//                 onClick={() =>

//                   WeekAppend({
//                     id: Date.now(),
//                     startDate: null,
//                     endDate: null,
//                     [`checked${day}`]: true,

//                   })
//                 }

//               >
//                 <PlusRoundIcon style={{ fontSize: 20 }} />
//               </button>
//             </div>
//             <div className="col-1 mt-3">
//               <Whisper
//                 placement="auto"
//                 trigger="click"
//                 speaker={
//                   <MenuPopover
//                     selectedWeek={selectedWeek}
//                     checkedDays={checkedDays}
//                     setCheckedDays={setCheckedDays}
//                     onSelect={handleApply}
//                   />
//                 }
//               >
//                 <Button onClick={() => handleCopyClick(day)}>
//                   <CopyIcon style={{ fontSize: 20, cursor: "pointer" }} />
//                 </Button>
//               </Whisper>
//             </div>
//           </div>
//         ))}
//       </div>
//     </div>
//   );
// };
// WeeklyHours.propTypes = {
//   register: PropTypes.func.isRequired,
//   setValue: PropTypes.func.isRequired,
//   errors: PropTypes.object.isRequired,
//   WeekAppend: PropTypes.func.isRequired,
//   WeekRemove: PropTypes.func.isRequired,
//   WeekFields: PropTypes.array.isRequired,
//   trigger: PropTypes.func.isRequired,
// };
// export default WeeklyHours;













/* eslint-disable react/prop-types */
/* eslint-disable react/display-name */

import { useEffect, useState } from "react";
import "rsuite/dist/rsuite.min.css";
import PlusRoundIcon from "@rsuite/icons/PlusRound";
import MinusRoundIcon from "@rsuite/icons/MinusRound";
import CopyIcon from "@rsuite/icons/Copy";
import { DatePicker, Stack, Checkbox } from "rsuite";
import PropTypes from "prop-types";
import { forwardRef } from "react";
import { Popover, Whisper, Button, Dropdown } from "rsuite";

const daysOfWeek = [
  "Sunday",
  "Monday",
  "Tuesday",
  "Wednesday",
  "Thursday",
  "Friday",
  "Saturday",
];

const MenuPopover = forwardRef(
  ({ selectedWeek, onSelect, checkedDays, setCheckedDays, ...rest }, ref) => {
    return (
      <Popover ref={ref} {...rest} full>
        <Dropdown.Menu>
          {daysOfWeek.map((day) => (
            <Dropdown.Item
              key={day}
              eventKey={day}
              onSelect={() =>
                setCheckedDays((prev) => ({ ...prev, [day]: !prev[day] }))
              }
            >
              <Checkbox
                checked={checkedDays[day] || false}
                disabled={day === selectedWeek}
              >
                {day}
              </Checkbox>
            </Dropdown.Item>
          ))}
          <Dropdown.Item eventKey="apply">
            <div className="p-2 text-end">
              <button
                className="btn btn-primary"
                onClick={() =>
                  onSelect(
                    Object.keys(checkedDays).filter((day) => checkedDays[day])
                  )
                }
              >
                Apply
              </button>
            </div>
          </Dropdown.Item>
        </Dropdown.Menu>
      </Popover>
    );
  }
);

const WeeklyHours = ({
  register,
  WeekAppend,
  watch,
  WeekRemove,
  WeekFields,
  errors,
  setValue,
  trigger,
}) => {
  const [selectedWeek, setSelectedWeek] = useState(null);
  const [checkedDays, setCheckedDays] = useState({});

  useEffect(() => {
    WeekFields.forEach((_, index) => {
      daysOfWeek.forEach((day) => {
        register(`data.${index}.${day}.startDate`, {
          required: "Start time is required",
        });
        register(`data.${index}.${day}.endDate`);
        register(`data.${index}.${day}.checked`);
      });
    });
  }, [WeekFields, register]);

  const handleToggle = (day) => {
    const isChecked = WeekFields.some((entry) => entry[day]?.checked);
    if (!isChecked) {
      WeekAppend({
        id: Date.now(),
        [day]: { startDate: null, endDate: null, checked: true },
      });
    }
  };

  const handleCopyClick = (day) => {
    const selectedEntry = WeekFields.find((entry) => entry[day]?.checked);

    if (selectedEntry) {
      setSelectedWeek(day);
      setCheckedDays({});
    }
  };

  const handleApply = (days) => {
    console.log("Checked Days:", days);

    if (!selectedWeek) return; // Exit if no day was selected

    // Find the selected week's data
    const selectedFields = WeekFields.find(
      (entry) => entry[selectedWeek]?.checked
    );

    if (!selectedFields || !selectedFields[selectedWeek]) return; // Exit if no valid data

    days.forEach((day) => {
      const existingIndex = WeekFields.findIndex(
        (entry) => entry[day]?.checked
      );

      if (existingIndex !== -1) {
        // ✅ Update existing day instead of appending a duplicate
        setValue(
          `data.${existingIndex}.${day}.startDate`,
          selectedFields[selectedWeek].startDate
        );
        setValue(
          `data.${existingIndex}.${day}.endDate`,
          selectedFields[selectedWeek].endDate
        );
        setValue(`data.${existingIndex}.${day}.checked`, true);

        // Ensure fields update
        trigger(`data.${existingIndex}.${day}.startDate`);
        trigger(`data.${existingIndex}.${day}.endDate`);
      } else {
        // ✅ Append new entry with copied data
        WeekAppend({
          id: Date.now(),
          [day]: {
            startDate: selectedFields[selectedWeek].startDate,
            endDate: selectedFields[selectedWeek].endDate,
            checked: true,
          },
        });
      }
    });

    console.log("Applied copied values:", days);
  };

  return (
    <div className="container mt-3 card">
      <div className="card-body">
        {daysOfWeek.map((day) => (
          <div className="p-1 row" key={day}>
            <div className="d-flex align-items-center col-2">
              <Checkbox
                checked={WeekFields.some((entry) => entry[day]?.checked)}
                onChange={() => handleToggle(day)}
              >
                {day}
              </Checkbox>
            </div>

            <div className="col-6">
              {WeekFields.some((entry) => entry[day]?.checked) ? (
                WeekFields.filter((entry) => entry[day]?.checked).map(
                  (item, index) => (
                    <div key={item.id} className="row mt-2">
                      <div className="col-md-4">
                        <label>Start time</label>
                        <Stack
                          direction="column"
                          alignItems="flex-start"
                          spacing={6}
                        >
                          <DatePicker
                            format="HH:mm"
                            editable={false}
                            value={
                              watch(`data.${index}.${day}.startDate`) || null
                            }
                            onChange={(date) => {
                              setValue(`data.${index}.${day}.startDate`, date);
                              trigger(`data.${index}.${day}.startDate`);
                            }}
                          />
                        </Stack>
                        {errors.data?.[index]?.[day]?.startDate && (
                          <p className="text-danger">
                            {errors.data[index][day].startDate.message}
                          </p>
                        )}
                      </div>

                      <div className="col-md-4">
                        <label>End time</label>
                        <Stack
                          direction="column"
                          alignItems="flex-start"
                          spacing={6}
                        >
                          <DatePicker
                            format="HH:mm"
                            editable={false}
                            value={
                              watch(`data.${index}.${day}.endDate`) || null
                            }
                            onChange={(date) => {
                              setValue(`data.${index}.${day}.endDate`, date);
                              trigger(`data.${index}.${day}.endDate`);
                            }}
                          />
                        </Stack>
                        {errors.data?.[index]?.[day]?.endDate && (
                          <p className="text-danger">
                            {errors.data[index][day].endDate.message}
                          </p>
                        )}
                      </div>

                      {/* Remove Button */}
                      <div className="mt-3 col-2 d-flex flex-row">
                        <button
                          type="button"
                          className="me-2"
                          onClick={() => {
                            const removeIndex = WeekFields.findIndex(
                              (field) => field.id === item.id
                            );
                            if (removeIndex !== -1) WeekRemove(removeIndex);
                          }}
                        >
                          <MinusRoundIcon style={{ fontSize: 15 }} />
                        </button>
                      </div>
                    </div>
                  )
                )
              ) : (
                <p className="pt-3">Unavailable</p>
              )}
            </div>

            {/* Add Time Slot Button */}
            <div className="col-2 mt-3 d-flex flex-row">
              <button
                type="button"
                onClick={() =>
                  WeekAppend({
                    id: Date.now(),
                    [day]: { startDate: null, endDate: null, checked: true },
                  })
                }
              >
                <PlusRoundIcon style={{ fontSize: 20 }} />
              </button>
            </div>

            {/* Copy Button */}
            <div className="col-1 mt-3">
              <Whisper
                placement="auto"
                trigger="click"
                speaker={
                  <MenuPopover
                    selectedWeek={selectedWeek}
                    checkedDays={checkedDays}
                    setCheckedDays={setCheckedDays}
                    onSelect={handleApply}
                  />
                }
              >
                <Button onClick={() => handleCopyClick(day)}>
                  <CopyIcon style={{ fontSize: 20, cursor: "pointer" }} />
                </Button>
              </Whisper>
            </div>
          </div>
        ))}
      </div>
    </div>
  );
};

WeeklyHours.propTypes = {
  register: PropTypes.func.isRequired,
  setValue: PropTypes.func.isRequired,
  errors: PropTypes.object.isRequired,
  WeekAppend: PropTypes.func.isRequired,
  WeekRemove: PropTypes.func.isRequired,
  WeekFields: PropTypes.array.isRequired,
  trigger: PropTypes.func.isRequired,
};

export default WeeklyHours;












//updated code...











/* eslint-disable react/prop-types */
/* eslint-disable react/display-name */
import { useEffect, useState } from "react";
import "rsuite/dist/rsuite.min.css";
import PlusRoundIcon from "@rsuite/icons/PlusRound";
import MinusRoundIcon from "@rsuite/icons/MinusRound";
import CopyIcon from "@rsuite/icons/Copy";
import { DatePicker, Stack, Checkbox } from "rsuite";
import PropTypes from "prop-types";
import { forwardRef } from "react";
import { Popover, Whisper, Button, Dropdown } from "rsuite";

const MenuPopover = forwardRef(
  ({ selectedWeek, onSelect, checkedDays, setCheckedDays, ...rest }, ref) => {
    return (
      <Popover ref={ref} {...rest} full>
        <Dropdown.Menu>
          {[
            "Sunday",
            "Monday",
            "Tuesday",
            "Wednesday",
            "Thursday",
            "Friday",
            "Saturday",
          ].map((day) => (
            <Dropdown.Item
              key={day}
              eventKey={day}
             
              onSelect={() =>
                setCheckedDays((prev) => ({ ...prev, [day]: !prev[day] }))
              }
            >
              <Checkbox
                checked={checkedDays[day] || day===selectedWeek}
                disabled={day === selectedWeek}
                
              >
                {day}
              </Checkbox> 
            </Dropdown.Item>
          ))}
          <Dropdown.Item eventKey="apply" >
            <button
              className="btn btn-primary"
              onClick={() =>
                onSelect(
                  Object.keys(checkedDays).filter((day) => checkedDays[day])
                )
              }
            >
              Apply
            </button>
          </Dropdown.Item>
        </Dropdown.Menu>
      </Popover>
    );
  }
);

const WeeklyHours = ({
  register,
  WeekAppend,
  watch,
  WeekRemove,
  WeekFields,
  errors,
  setValue,
  trigger,
}) => {
  const [selectedWeek, setSelectedWeek] = useState(null);
  const [checkedDays, setCheckedDays] = useState({});

  useEffect(() => {
    WeekFields.forEach((_, index) => {
      register(`data.${index}.startDate`, {
        required: "Start time is required",
      });
      register(`data.${index}.endDate`, { required: "End time is required" });
      [
        "Sunday",
        "Monday",
        "Tuesday",
        "Wednesday",
        "Thursday",
        "Friday",
        "Saturday",
      ].forEach((day) => {
        register(`data.${index}.checked${day}`);
      });
    });
  }, [WeekFields, register]);

  const handleToggle = (day) => {
    const isChecked = WeekFields.some((entry) => entry[`checked${day}`]);

    if (!isChecked) {
      WeekAppend({
        id: Date.now(),
        startDate: null,
        endDate: null,
        [`checked${day}`]: true,
      });
    } else {
      ("");
    }
  };

  const handleCopyClick = (day) => {
    setSelectedWeek(day);
    setCheckedDays({});
  };

 
  const handleApply = (days) => {
    console.log("Checked Days:", days);
    
    const selectedFields = WeekFields.filter((entry) => entry[`checked${selectedWeek}`]);
  
    if (selectedFields.length === 0) return;
  
    days.forEach((day) => {
      selectedFields.forEach((field) => {
        WeekAppend({
          id: Date.now(),
          startDate: field.startDate,
          endDate: field.endDate,
          [`checked${day}`]: true,
        });
      });
    });
  
  };
  

  return (
    <div className="container mt-3 card">
      <div className="card-body">
        {[
          "Sunday",
          "Monday",
          "Tuesday",
          "Wednesday",
          "Thursday",
          "Friday",
          "Saturday",
        ].map((day) => (
          <div className="p-1 row" key={day}>
            <div className="d-flex align-items-center col-2">
              <Checkbox
                checked={WeekFields.some((entry) => entry[`checked${day}`])}
                onChange={() => handleToggle(day)}
              >
                {day}
              </Checkbox>
            </div>
            <div className="col-6">
              {WeekFields.some((entry) => entry[`checked${day}`]) ? (
                WeekFields.filter((entry) => entry[`checked${day}`]).map(
                  (item, index) => (
                    <div key={item.id} className="row mt-2">
                      <div className="col-md-4">
                        <label>Start time</label>
                        <Stack
                          direction="column"
                          alignItems="flex-start"
                          spacing={6}
                        >
                          <DatePicker
                            format="HH:mm"
                            editable={false}
                            value={watch(`data.${index}.startDate`) || null}
                            onChange={(date) => {
                              setValue(`data.${index}.startDate`, date);
                              trigger(`data.${index}.startDate`);
                            }}
                          />
                        </Stack>
                        {errors.data?.[index]?.startDate && (
                          <p className="text-danger">
                            {errors.data[index].startDate.message}
                          </p>
                        )}
                      </div>
                      <div className="col-md-4">
                        <label>End time</label>
                        <Stack
                          direction="column"
                          alignItems="flex-start"
                          spacing={6}
                        >
                          <DatePicker
                            format="HH:mm"
                            editable={false}
                            value={watch(`data.${index}.endDate`) || null}
                            onChange={(date) => {
                              setValue(`data.${index}.endDate`, date);
                              trigger(`data.${index}.endDate`);
                            }}
                          />
                        </Stack>
                        {errors.data?.[index]?.endDate && (
                          <p className="text-danger">
                            {errors.data[index].endDate.message}
                          </p>
                        )}
                      </div>
                      <div className="mt-3 col-2 d-flex flex-row">
                        <button
                          type="button"
                          className="me-2"
                          onClick={() => {
                            const removeIndex = WeekFields.findIndex((field) => field.id === item.id);
                            if (removeIndex !== -1) {
                              WeekRemove(removeIndex);
                            }
                          }}
                        >
                          <MinusRoundIcon style={{ fontSize: 15 }} />
                        </button>
                      </div>
                    </div>
                  )
                )
              ) : (
                <p className="pt-3">Unavailable</p>
              )}
            </div>
            <div className="col-2 mt-3 d-flex flex-row">
              <button
                type="button"
                onClick={() =>
                  WeekAppend({
                    id: Date.now(),
                    startDate: null,
                    endDate: null,
                    [`checked${day}`]: true,
                  })
                }
              >
                <PlusRoundIcon style={{ fontSize: 20 }} />
              </button>
            </div>
            <div className="col-1 mt-3">
              <Whisper
                placement="auto"
                trigger="click"
                speaker={
                  <MenuPopover
                    selectedWeek={selectedWeek}
                    checkedDays={checkedDays}
                    setCheckedDays={setCheckedDays}
                    onSelect={handleApply}
                  />
                }
              >
                <Button onClick={() => handleCopyClick(day)}>
                  <CopyIcon style={{ fontSize: 20, cursor: "pointer" }} />
                </Button>
              </Whisper>
            </div>
          </div>
        ))}
      </div>
    </div>

    
  );
};

WeeklyHours.propTypes = {
  register: PropTypes.func.isRequired,
  setValue: PropTypes.func.isRequired,
  errors: PropTypes.object.isRequired,
  WeekAppend: PropTypes.func.isRequired,
  WeekRemove: PropTypes.func.isRequired,
  WeekFields: PropTypes.array.isRequired,
  trigger: PropTypes.func.isRequired,
};

export default WeeklyHours;



















// /* eslint-disable react/prop-types */
// /* eslint-disable react/display-name */
// import { useEffect, useState } from "react";
// import "rsuite/dist/rsuite.min.css";
// import PlusRoundIcon from "@rsuite/icons/PlusRound";
// import MinusRoundIcon from "@rsuite/icons/MinusRound";
// import CopyIcon from "@rsuite/icons/Copy";
// import { DatePicker, Stack, Checkbox } from "rsuite";
// import PropTypes from "prop-types";
// import { forwardRef } from "react";
// import { Popover, Whisper, Button, Dropdown } from "rsuite";

// const MenuPopover = forwardRef(
//   ({ selectedWeek, onSelect, onApply, checkedWeeks, ...rest }, ref) => (
//     <Popover ref={ref} {...rest}>
//       <Dropdown.Menu>
//         {[
//           "Sunday",
//           "Monday",
//           "Tuesday",
//           "Wednesday",
//           "Thursday",
//           "Friday",
//           "Saturday",
//         ].map((day) => (
//           <Dropdown.Item key={day} eventKey={day} onClick={() => onSelect(day)}>
//             <Checkbox
//               disabled={checkedWeeks.includes(day) || day === selectedWeek}
//             >
//               {day}
//             </Checkbox>
//           </Dropdown.Item>
//         ))}
//         <Dropdown.Item>
//           <button className="btn btn-primary" onClick={onApply}>
//             Apply
//           </button>
//         </Dropdown.Item>
//       </Dropdown.Menu>
//     </Popover>
//   )
// );

// const WeeklyHours = ({
//   register,
//   WeekAppend,
//   WeekRemove,
//   WeekFields,
//   errors,
//   setValue,
//   trigger,
//   watch
// }) => {
//   const [selectedWeek, setSelectedWeek] = useState(null);
//   const [copiedTimes, setCopiedTimes] = useState({
//     starttime: null,
//     endtime: null,
//   });
//   const [checkedWeeks, setCheckedWeeks] = useState([]);

//   useEffect(() => {
//     WeekFields.forEach((_, index) => {
//       register(`data.${index}.starttime`);
//       register(`data.${index}.endtime`);
//     });
//   }, [WeekFields, register]);

//   const handleToggle = (day) => {
//     const isChecked = WeekFields.some((entry) => entry[`checked${day}`]);

//     if (!isChecked) {
//       WeekAppend({
//         id: Date.now(),
//         starttime: copiedTimes.starttime || null,
//         endtime: copiedTimes.endtime || null,
//         [`checked${day}`]: true,
//       });
//     } else {
//       const indicesToRemove = WeekFields.filter(
//         (entry) => entry[`checked${day}`]
//       ).map((entry) => entry.id);
//       indicesToRemove.forEach((id) => {
//         const indexToRemove = WeekFields.findIndex((entry) => entry.id === id);
//         if (indexToRemove !== -1) WeekRemove(indexToRemove);
//       });
//     }
//   };

//   const handleCopyWeek = (day) => {
//     const copiedWeek = WeekFields.find((entry) => entry[`checked${day}`]);
//     if (copiedWeek) {
//       setCopiedTimes({
//         starttime: copiedWeek.starttime,
//         endtime: copiedWeek.endtime,
//       });
//       setSelectedWeek(day);
//     }
//   };

//   const renderDaySection = (day) => {
//     const isChecked = WeekFields.some((entry) => entry[`checked${day}`]);
//     return (
//       <div className="p-1 row" key={day}>
//         <div className="d-flex align-items-center col-2">
//           <Checkbox checked={isChecked} onChange={() => handleToggle(day)}>
//             {day}
//           </Checkbox>
//         </div>
//         <div className="col-6">
//           {isChecked ? (
//             WeekFields.filter((entry) => entry[`checked${day}`]).map(
//               (item, index) => (
//                 <div key={item.id} className="row mt-2">
//                   <div className="col-md-4">
//                     <label>Start time</label>
//                     <Stack
//                       direction="column"
//                       alignItems="flex-start"
//                       spacing={6}
//                     >
//                       <DatePicker
//                       format="HH:mm"
//                       editable={false}
//                       value={watch(`data.${index}.starttime`) || null}
//                       onChange={(date) => {
//                         setValue(`data.${index}.starttime`, date, { shouldValidate: true, shouldDirty: true });
//                         trigger(`data.${index}.starttime`);
//                       }}


//                     />

//                     </Stack>
//                     {errors.data?.[index]?.starttime && (
//                       <p className="text-danger" style={{ fontSize: "12px" }}>
//                         {errors.data[index].starttime.message}
//                       </p>
//                     )}
//                   </div>
//                   <div className="col-md-4">
//                     <label>End time</label>
//                     <Stack
//                       direction="column"
//                       alignItems="flex-start"
//                       spacing={6}
//                     >
//                       <DatePicker
//                         format="HH:mm"
//                         editable={false}
//                         value={watch(`data.${index}.endtime`) || null}
//                         onChange={(date) => {
//                           setValue(`data.${index}.endtime`, date, {
//                             shouldValidate: true,
//                             shouldDirty: true,
//                           });
//                           trigger(`data.${index}.endtime`);
//                         }}
//                       />
//                     </Stack>
//                     {errors.data?.[index]?.endtime && (
//                       <p className="text-danger" style={{ fontSize: "12px" }}>
//                         {errors.data[index].endtime.message}
//                       </p>
//                     )}
//                   </div>
//                   <div className="mt-3 col-2 d-flex flex-row">
//                     <button
//                       type="button"
//                       className="me-2"
//                       onClick={() => handleToggle(day)}
//                     >
//                       <MinusRoundIcon style={{ fontSize: 15 }} />
//                     </button>
//                   </div>
//                 </div>
//               )
//             )
//           ) : (
//             <p className="pt-3">Unavailable</p>
//           )}
//         </div>
//         <div className="col-2 mt-3 d-flex flex-row">
//           <button type="button" onClick={() => handleToggle(day)}>
//             <PlusRoundIcon style={{ fontSize: 20 }} />
//           </button>
//         </div>
//         <div className="col-1 mt-3">
//           <Whisper
//             placement="auto"
//             controlId={`popover-${day}`}
//             trigger="click"
//             speaker={
//               <MenuPopover
//                 selectedWeek={selectedWeek}
//                 checkedWeeks={checkedWeeks}
//                 onSelect={handleToggle}
//                 onApply={() => {}}
//               />
//             }
//           >
//             <Button onClick={() => handleCopyWeek(day)}>
//               <CopyIcon style={{ fontSize: 20, cursor: "pointer" }} />
//             </Button>
//           </Whisper>
//         </div>
//       </div>
//     );
//   };
//   return (
//     <div className="container mt-3 card">
//       <div className="card-body">
//         {[
//           "Sunday",
//           "Monday",
//           "Tuesday",
//           "Wednesday",
//           "Thursday",
//           "Friday",
//           "Saturday",
//         ].map((day) => renderDaySection(day))}
//       </div>
//     </div>
//   );
// };

// WeeklyHours.propTypes = {
//   register: PropTypes.func.isRequired,
//   setValue: PropTypes.func.isRequired,
//   errors: PropTypes.object.isRequired,
//   WeekAppend: PropTypes.func.isRequired,
//   WeekRemove: PropTypes.func.isRequired,
//   WeekFields: PropTypes.array.isRequired,
//   trigger: PropTypes.func.isRequired,
// };

// export default WeeklyHours;














upadated code    












/* eslint-disable react/prop-types */
/* eslint-disable react/display-name */
import { useEffect, useState } from "react";
import "rsuite/dist/rsuite.min.css";
import PlusRoundIcon from "@rsuite/icons/PlusRound";
import MinusRoundIcon from "@rsuite/icons/MinusRound";
import CopyIcon from "@rsuite/icons/Copy";
import { DatePicker, Stack, Checkbox } from "rsuite";
import PropTypes from "prop-types";
import { forwardRef } from "react";
import { Popover, Whisper, Button, Dropdown } from "rsuite";

const MenuPopover = forwardRef(
  ({ selectedWeek, onSelect, checkedDays, setCheckedDays, ...rest }, ref) => {
    return (
      <Popover ref={ref} {...rest} full>
        <Dropdown.Menu>
          {[
            "Sunday",
            "Monday",
            "Tuesday",
            "Wednesday",
            "Thursday",
            "Friday",
            "Saturday",
          ].map((day) => (
            <Dropdown.Item
              key={day}
              eventKey={day}
              onSelect={() =>
                setCheckedDays((prev) => ({ ...prev, [day]: !prev[day] }))
              }
            >
              <Checkbox
                checked={checkedDays[day] || day === selectedWeek}
                disabled={day === selectedWeek}
              >
                {day}
              </Checkbox>
            </Dropdown.Item>
          ))}
          <Dropdown.Item eventKey="apply">
            <button
              className="btn btn-primary"
              onClick={() =>
                onSelect(
                  Object.keys(checkedDays).filter((day) => checkedDays[day])
                )
              }
            >
              Apply
            </button>
          </Dropdown.Item>
        </Dropdown.Menu>
      </Popover>
    );
  }
);

const WeeklyHours = ({
  register,
  WeekAppend,
  watch,
  WeekRemove,
  WeekFields,
  errors,
  setValue,
  trigger,
  getValues,
}) => {
  const [selectedWeek, setSelectedWeek] = useState(null);
  const [checkedDays, setCheckedDays] = useState({});

  useEffect(() => {
    WeekFields.forEach((item) => {
      register(`WeekFields.${item.id}.startDate`, {
        required: "Start time is required",
      });
      register(`WeekFields.${item.id}.endDate`, {
        required: "End time is required",
      });

      [
        "Sunday",
        "Monday",
        "Tuesday",
        "Wednesday",
        "Thursday",
        "Friday",
        "Saturday",
      ].forEach((day) => {
        register(`WeekFields.${item.id}.checked${day}`);
      });
    });
  }, [WeekFields, register]);

  const handleToggle = (day) => {
    const isChecked = WeekFields.some((entry) => entry[`checked${day}`]);
    console.log(isChecked, "ischeckedddddddddddddddd");
    if (!isChecked) {
      WeekAppend({
        id: Date.now(),
        startDate: null,
        endDate: null,
        [`checked${day}`]: true,
      });
    } else {
      ("");
    }
  };

  const handleCopyClick = (day) => {
    const selectedField = WeekFields.find((entry) => entry[`checked${day}`]);

    if (!selectedField) return;

    setSelectedWeek(day);
    setCheckedDays({});
  };

  const handleApply = (days) => {
    console.log("Checked Days:", days);

    const selectedField = WeekFields.find(
      (entry) => entry[`checked${selectedWeek}`]
    );
    console.log(WeekFields, "fffffffffffff");
    console.log(selectedField, "selectedfieldsssssssssssssssss");
    if (!selectedField) return;

    days.forEach((day) => {
      const existingField = WeekFields.find((entry) =>
        Object.keys(entry).some((key) => key === `checked${day}`)
      );

      console.log(existingField, "Found Existing Field");

      if (existingField) {
        setValue(
          `WeekFields.${existingField.id}.startDate`,
          selectedField.startDate
        );
        setValue(
          `WeekFields.${existingField.id}.endDate`,
          selectedField.endDate
        );
        setValue(`WeekFields.${existingField.id}.checked${day}`, true);
      } else {
        WeekAppend({
          id: Date.now(),
          startDate: selectedField.startDate,
          endDate: selectedField.endDate,
          [`checked${day}`]: true,
        });
      }
    });
  };

  return (
    <div className="container mt-3 card">
      <div className="card-body">
        {[
          "Sunday",
          "Monday",
          "Tuesday",
          "Wednesday",
          "Thursday",
          "Friday",
          "Saturday",
        ].map((day) => (
          <div className="p-1 row" key={day}>
            <div className="d-flex align-items-center col-2">
              <Checkbox
                checked={WeekFields.some((entry) => entry[`checked${day}`])}
                onChange={() => handleToggle(day)}
              >
                {day}
              </Checkbox>
            </div>
            <div className="col-6">
              {WeekFields.some((entry) => entry[`checked${day}`]) ? (
                WeekFields.filter((entry) => entry[`checked${day}`]).map(
                  (item, index) => (
                    <div key={item.id} className="row mt-2">
                      <div className="col-md-4">
                        <label>Start time</label>
                        <Stack
                          direction="column"
                          alignItems="flex-start"
                          spacing={6}
                        >
                          <DatePicker
                            format="HH:mm"
                            editable={false}
                            value={
                              watch(`WeekFields.${item.id}.startDate`) ||
                              `WeekFields.${index}.startDate`
                            }
                            onChange={(date) => {
                              setValue(`WeekFields.${item.id}.startDate`, date);
                              trigger(`WeekFields.${item.id}.startDate`);
                            }}
                          />
                        </Stack>
                        {errors.WeekFields?.[index]?.startDate && (
                          <p className="text-danger">
                            {errors.WeekFields[index].startDate.message}
                          </p>
                        )}
                      </div>
                      <div className="col-md-4">
                        <label>End time</label>
                        <Stack
                          direction="column"
                          alignItems="flex-start"
                          spacing={6}
                        >
                          <DatePicker
                            format="HH:mm"
                            editable={false}
                            value={
                              watch(`WeekFields.${item.id}.endDate`) ||
                              `WeekFields.${index}.endDate`
                            }
                            onChange={(date) => {
                              setValue(`WeekFields.${item.id}.endDate`, date);
                              trigger(`WeekFields.${item.id}.endDate`);
                            }}
                          />
                        </Stack>
                        {errors.WeekFields?.[index]?.endDate && (
                          <p className="text-danger">
                            {errors.WeekFields[index].endDate.message}
                          </p>
                        )}
                      </div>
                      <div className="mt-3 col-2 d-flex flex-row">
                        <button
                          type="button"
                          className="me-2"
                          onClick={() => {
                            const removeIndex = WeekFields.findIndex(
                              (field) => field.id === item.id
                            );
                            if (removeIndex !== -1) {
                              WeekRemove(removeIndex);
                            }
                          }}
                        >
                          <MinusRoundIcon style={{ fontSize: 15 }} />
                        </button>
                      </div>
                    </div>
                  )
                )
              ) : (
                <p className="pt-3">Unavailable</p>
              )}
            </div>
            <div className="col-2 mt-3 d-flex flex-row">
              <button
                type="button"
                onClick={() =>
                  WeekAppend({
                    id: Date.now(),
                    startDate: null,
                    endDate: null,
                    [`checked${day}`]: true,
                  })
                }
              >
                <PlusRoundIcon style={{ fontSize: 20 }} />
              </button>
            </div>
            <div className="col-1 mt-3">
              <Whisper
                placement="auto"
                trigger="click"
                speaker={
                  <MenuPopover
                    selectedWeek={selectedWeek}
                    checkedDays={checkedDays}
                    setCheckedDays={setCheckedDays}
                    onSelect={handleApply}
                  />
                }
              >
                <Button onClick={() => handleCopyClick(day)}>
                  <CopyIcon style={{ fontSize: 20, cursor: "pointer" }} />
                </Button>
              </Whisper>
            </div>
          </div>
        ))}
      </div>
    </div>
  );
};

WeeklyHours.propTypes = {
  register: PropTypes.func.isRequired,
  setValue: PropTypes.func.isRequired,
  errors: PropTypes.object.isRequired,
  WeekAppend: PropTypes.func.isRequired,
  WeekRemove: PropTypes.func.isRequired,
  WeekFields: PropTypes.array.isRequired,
  trigger: PropTypes.func.isRequired,
};

export default WeeklyHours;



















//upadted working







/* eslint-disable react/prop-types */
/* eslint-disable react/display-name */
import { DateTime } from "luxon";
import { useEffect, useState } from "react";
import "rsuite/dist/rsuite.min.css";
import PlusRoundIcon from "@rsuite/icons/PlusRound";
import MinusRoundIcon from "@rsuite/icons/MinusRound";
import CopyIcon from "@rsuite/icons/Copy";
import { DatePicker, Checkbox } from "rsuite";
import { forwardRef } from "react";
import { Popover, Whisper, Button, Dropdown } from "rsuite";

const daysOfWeek = [
  "Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"
];
const MenuPopover = forwardRef(({ selectedWeek, onSelect, checkedDays, setCheckedDays, ...rest }, ref) => (
  <Popover ref={ref} {...rest} full>
    <Dropdown.Menu>
      {daysOfWeek.map((day) => (
        <Dropdown.Item
          key={day}
          eventKey={day}
          onSelect={() => setCheckedDays((prev) => ({ ...prev, [day]: !prev[day] }))}
        >
          <Checkbox checked={checkedDays[day] || day === selectedWeek} disabled={day === selectedWeek}>
            {day}
          </Checkbox>
        </Dropdown.Item>
      ))}
      <Dropdown.Item eventKey="apply">
        <button className="btn btn-primary" onClick={() => onSelect(Object.keys(checkedDays).filter((day) => checkedDays[day]))}>
          Apply
        </button>
      </Dropdown.Item>
    </Dropdown.Menu>
  </Popover>
));

const WeeklyHours = ({ register, WeekAppend, watch, WeekRemove, WeekFields, errors, setValue, trigger, getValues }) => {
  const [selectedWeek, setSelectedWeek] = useState(null);
  const [checkedDays, setCheckedDays] = useState({});

  useEffect(() => {
    WeekFields.forEach((_, index) => {
      daysOfWeek.forEach((day) => {
        register(`WeekFields[${index}].${day}.startDate`, { required: "Start time is required" });
        register(`WeekFields[${index}].${day}.endDate`, { required: "End time is required" });
        register(`WeekFields[${index}].${day}.checked`, {});
      });
    });
  }, [WeekFields, register]);

  const handleCopyClick = (day) => {
    setSelectedWeek(day);
    setCheckedDays({});
  };



const handleApply = async (days) => {
  const sourceIndex = WeekFields.findIndex((entry) => entry[selectedWeek]?.checked);
  if (sourceIndex === -1) return;

  const currentValues = getValues();
  console.log("Current Form Values:", currentValues);

  let sourceStartTime = currentValues.WeekFields?.[sourceIndex]?.[selectedWeek]?.startDate || null;
  let sourceEndTime = currentValues.WeekFields?.[sourceIndex]?.[selectedWeek]?.endDate || null;

  console.log(" Source Start Time Before Fix:", sourceStartTime);
  console.log(" Source End Time Before Fix:", sourceEndTime);

  sourceStartTime = sourceStartTime ? DateTime.fromJSDate(new Date(sourceStartTime)) : null;
  sourceEndTime = sourceEndTime ? DateTime.fromJSDate(new Date(sourceEndTime)) : null;

  if (!sourceStartTime || !sourceEndTime) {
    console.error("Missing Start or End Time. Copy aborted.");
    return;
  }

  const getFixedTime = (date) => {
    return DateTime.now().set({ hour: date.hour, minute: date.minute, second: 0, millisecond: 0 }).toJSDate();
  };

  const formattedStartTime = getFixedTime(sourceStartTime);
  const formattedEndTime = getFixedTime(sourceEndTime);

  console.log(" Formatted Start Time:", formattedStartTime);
  console.log(" Formatted End Time:", formattedEndTime);

  for (const day of days) {
    let targetIndex = WeekFields.findIndex((entry) => entry[day]?.checked);

    if (targetIndex === -1) {
      console.log(` Adding new entry for ${day}`);

     
      await new Promise((resolve) => {
        WeekAppend({ [day]: { checked: true, startDate: null, endDate: null } });
        setTimeout(resolve, 0); 
      });

      targetIndex = WeekFields.length; 
    }

    console.log(` Updating ${day} at index ${targetIndex}`);

    setValue(`WeekFields[${targetIndex}].${day}.startDate`, formattedStartTime, { shouldDirty: true, shouldTouch: true, shouldValidate: true });
    setValue(`WeekFields[${targetIndex}].${day}.endDate`, formattedEndTime, { shouldDirty: true, shouldTouch: true, shouldValidate: true });

    trigger(`WeekFields[${targetIndex}].${day}.startDate`);
    trigger(`WeekFields[${targetIndex}].${day}.endDate`);

    console.log("Values Set for", day, "at index", targetIndex);
  }

  console.log("Copy  Successfully");
};


  return (
    <div className="container mt-3 card">
      <div className="card-body">
        {daysOfWeek.map((day) => (
          // <div>
          <div className="p-1 row" key={day}>
            <div className="d-flex align-items-center col-2 ">
              <Checkbox
                checked={WeekFields.some((entry) => entry[day]?.checked)}
                onChange={() => WeekAppend({ [day]: { checked: true , startDate: null, endDate: null } })}
              >
                {day}
              </Checkbox>
            </div>
            <div className="col-6">
              {WeekFields.some((entry) => entry[day]?.checked) ? (
                WeekFields.map((item, index) =>
                  item[day]?.checked ? (
                    <div key={index} className="row mt-2">
                      <div className="col-md-4">
                        <label>Start time</label>
                        <DatePicker
                          format="HH:mm"
                          editable={false}
                          value={watch(`WeekFields[${index}].${day}.startDate`)}
                          onChange={(date) => {
                            setValue(`WeekFields[${index}].${day}.startDate`, date);
                            trigger(`WeekFields[${index}].${day}.startDate`);
                          }}
                        />
                        {errors.WeekFields?.[index]?.[day]?.startDate && <p className="text-danger">{errors.WeekFields[index][day].startDate.message}</p>}
                      </div>
                      <div className="col-md-4">
                        <label>End time</label>
                        <DatePicker
                          format="HH:mm"
                          editable={false}
                          value={watch(`WeekFields[${index}].${day}.endDate`)}
                          onChange={(date) => {
                            setValue(`WeekFields[${index}].${day}.endDate`, date);
                            trigger(`WeekFields[${index}].${day}.endDate`);
                          }}
                        />
                        {errors.WeekFields?.[index]?.[day]?.endDate && <p className="text-danger">{errors.WeekFields[index][day].endDate.message}</p>}
                      </div>
                      <div className="mt-3 col-2">
                        <button type="button" onClick={() => WeekRemove(index)}>
                          <MinusRoundIcon style={{ fontSize: 15 }} />
                        </button>
                      </div>
                    </div>
                  ) : null
                )
              ) : (
                <p className="pt-3">Unavailable</p>
              )}
            </div>
            <div className="col-2 mt-3">
              <button type="button" onClick={() => WeekAppend({ [day]: { checked: true, startDate: null, endDate: null } })}>
                <PlusRoundIcon style={{ fontSize: 20 }} />
              </button>
            </div>
            <div className="col-1 mt-3">
              <Whisper
                placement="auto"
                trigger="click"
                speaker={<MenuPopover selectedWeek={selectedWeek} checkedDays={checkedDays} setCheckedDays={setCheckedDays} onSelect={handleApply} />}
              >
                <Button onClick={() => handleCopyClick(day)}>
                  <CopyIcon style={{ fontSize: 20, cursor: "pointer" }} />
                </Button>
              </Whisper>
            </div>
          </div>
        ))}
      </div>
    </div>
  );
};

export default WeeklyHours;















upadated






/* eslint-disable react/prop-types */
/* eslint-disable react/display-name */
import { DateTime } from "luxon";
import { useEffect, useState } from "react";
import "rsuite/dist/rsuite.min.css";
import PlusRoundIcon from "@rsuite/icons/PlusRound";
import MinusRoundIcon from "@rsuite/icons/MinusRound";
import CopyIcon from "@rsuite/icons/Copy";
import { DatePicker, Checkbox } from "rsuite";
import { forwardRef } from "react";
import { Popover, Whisper, Button, Dropdown } from "rsuite";

const daysOfWeek = [
  "Sunday",
  "Monday",
  "Tuesday",
  "Wednesday",
  "Thursday",
  "Friday",
  "Saturday",
];
const MenuPopover = forwardRef(
  ({ selectedWeek, onSelect, checkedDays, setCheckedDays, ...rest }, ref) => (
    <Popover ref={ref} {...rest} full>
      <Dropdown.Menu>
        {daysOfWeek.map((day) => (
          <Dropdown.Item
            key={day}
            eventKey={day}
            onSelect={() =>
              setCheckedDays((prev) => ({ ...prev, [day]: !prev[day] }))
            }
          >
            <Checkbox
              checked={checkedDays[day] || day === selectedWeek}
              disabled={day === selectedWeek}
            >
              {day}
            </Checkbox>
          </Dropdown.Item>
        ))}
        <Dropdown.Item eventKey="apply">
          <button
            className="btn btn-primary"
            onClick={() =>
              onSelect(
                Object.keys(checkedDays).filter((day) => checkedDays[day])
              )
            }
          >
            Apply
          </button>
        </Dropdown.Item>
      </Dropdown.Menu>
    </Popover>
  )
);

const WeeklyHours = ({
  register,
  WeekAppend,
  watch,
  WeekRemove,
  WeekFields,
  errors,
  setValue,
  trigger,
  getValues,
}) => {
  const [selectedWeek, setSelectedWeek] = useState(null);
  const [checkedDays, setCheckedDays] = useState({});

  useEffect(() => {
    WeekFields.forEach((_, index) => {
      daysOfWeek.forEach((day) => {
        register(`WeekFields[${index}].${day}.startDate`, {
          required: "Start time is required",
        });
        register(`WeekFields[${index}].${day}.endDate`, {
          required: "End time is required",
        });
        register(`WeekFields[${index}].${day}.checked`, {});
      });
    });
  }, [WeekFields, register]);

  const handleCopyClick = (day) => {
    setSelectedWeek(day);
    setCheckedDays({});
  };

  const handleApply = async (days) => {
    const sourceIndex = WeekFields.findIndex(
      (entry) => entry[selectedWeek]?.checked
    );
    if (sourceIndex === -1) return;

    const currentValues = getValues();
    console.log("Current Form Values:", currentValues);

    let sourceStartTime =
      currentValues.WeekFields?.[sourceIndex]?.[selectedWeek]?.startDate ||
      null;
    let sourceEndTime =
      currentValues.WeekFields?.[sourceIndex]?.[selectedWeek]?.endDate || null;

    console.log(" Source Start Time Before Fix:", sourceStartTime);
    console.log(" Source End Time Before Fix:", sourceEndTime);

    sourceStartTime = sourceStartTime
      ? DateTime.fromJSDate(new Date(sourceStartTime))
      : null;
    sourceEndTime = sourceEndTime
      ? DateTime.fromJSDate(new Date(sourceEndTime))
      : null;

    if (!sourceStartTime || !sourceEndTime) {
      console.error("Missing Start or End Time. Copy aborted.");
      return;
    }

    const getFixedTime = (date) => {
      return DateTime.now()
        .set({
          hour: date.hour,
          minute: date.minute,
          second: 0,
          millisecond: 0,
        })
        .toJSDate();
    };

    const formattedStartTime = getFixedTime(sourceStartTime);
    const formattedEndTime = getFixedTime(sourceEndTime);

    console.log(" Formatted Start Time:", formattedStartTime);
    console.log(" Formatted End Time:", formattedEndTime);

    for (const day of days) {
      let targetIndex = WeekFields.findIndex((entry) => entry[day]?.checked);

      if (targetIndex === -1) {
        console.log(` Adding new entry for ${day}`);

        await new Promise((resolve) => {
          WeekAppend({
            [day]: { checked: true, startDate: null, endDate: null },
          });
          setTimeout(resolve);
        });

        targetIndex = WeekFields.length;
      }

      console.log(` Updating ${day} at index ${targetIndex}`);

      setValue(
        `WeekFields[${targetIndex}].${day}.startDate`,
        formattedStartTime,
        { shouldDirty: true, shouldTouch: true, shouldValidate: true }
      );
      setValue(`WeekFields[${targetIndex}].${day}.endDate`, formattedEndTime, {
        shouldDirty: true,
        shouldTouch: true,
        shouldValidate: true,
      });

      trigger(`WeekFields[${targetIndex}].${day}.startDate`);
      trigger(`WeekFields[${targetIndex}].${day}.endDate`);

      console.log("Values Set for", day, "at index", targetIndex);
    }

    console.log("Copy  Successfully");
  };

  const handleCheckboxChange = (day) => {
    const isChecked = WeekFields.some((entry) => entry[day]?.checked);
  
    if (!isChecked) {
      WeekAppend({
        [day]: { checked: true, startDate: null, endDate: null },
      });
    } else {
      const index = WeekFields.findIndex((entry) => entry[day]?.checked);
      if (index !== -1) {
        WeekRemove();
      }
    }
  };
  
  const handleAppend = (day) => {
    const currentValues = getValues("WeekFields") || [];
    
    const exists = currentValues.some((entry) => entry[day]?.checked);
  
    if (!exists) {
      WeekAppend({
        [day]: { checked: true, startDate: null, endDate: null },
      });
    }
  };
  

  return (
    <div className="container mt-3 card">
      <div className="card-body">
        {daysOfWeek.map((day) => (
        
          <div className="p-1 row" key={day}>
            <div className="d-flex align-items-center col-2 ">
              <Checkbox
                checked={WeekFields.some((entry) => entry[day]?.checked)}
                onChange={() => handleCheckboxChange(day)}
              >
                {day}
              </Checkbox>
            </div>
            <div className="col-6">
              {WeekFields.some((entry) => entry[day]?.checked) ? (
                WeekFields.map((item, index) =>
                  item[day]?.checked ? (
                    <div key={index} className="row mt-2">
                      <div className="col-md-4">
                        <label>Start time</label>
                        <DatePicker
                          format="HH:mm"
                          editable={false}
                          value={watch(`WeekFields[${index}].${day}.startDate`)}
                          onChange={(date) => {
                            setValue(
                              `WeekFields[${index}].${day}.startDate`,
                              date
                            );
                            trigger(`WeekFields[${index}].${day}.startDate`);
                          }}
                        />
                        {errors.WeekFields?.[index]?.[day]?.startDate && (
                          <p className="text-danger">
                            {errors.WeekFields[index][day].startDate.message}
                          </p>
                        )}
                      </div>
                      <div className="col-md-4">
                        <label>End time</label>
                        <DatePicker
                          format="HH:mm"
                          editable={false}
                          value={watch(`WeekFields[${index}].${day}.endDate`)}
                          onChange={(date) => {
                            setValue(
                              `WeekFields[${index}].${day}.endDate`,
                              date
                            );
                            trigger(`WeekFields[${index}].${day}.endDate`);
                          }}
                        />
                        {errors.WeekFields?.[index]?.[day]?.endDate && (
                          <p className="text-danger">
                            {errors.WeekFields[index][day].endDate.message}
                          </p>
                        )}
                      </div>
                      <div className="mt-3 col-2">
                        <button type="button" onClick={() => WeekRemove(index)}>
                          <MinusRoundIcon style={{ fontSize: 15 }} />
                        </button>
                      </div>
                    </div>
                  ) : null
                )
              ) : (
                <p className="pt-3">Unavailable</p>
              )}
            </div>
            <div className="col-2 mt-3">
              <button type="button" onClick={() => handleAppend(day)}>
                <PlusRoundIcon style={{ fontSize: 20 }} />
              </button>
            </div>
            <div className="col-1 mt-3">
              <Whisper
                placement="auto"
                trigger="click"
                speaker={
                  <MenuPopover
                    selectedWeek={selectedWeek}
                    checkedDays={checkedDays}
                    setCheckedDays={setCheckedDays}
                    onSelect={handleApply}
                  />
                }
              >
                <Button onClick={() => handleCopyClick(day)}>
                  <CopyIcon style={{ fontSize: 20, cursor: "pointer" }} />
                </Button>
              </Whisper>
            </div>
          </div>
        ))}
      </div>
    </div>
  );
};

export default WeeklyHours;

































import { Modal, ButtonToolbar, Button } from "rsuite";
import { useState } from "react";
import "rsuite/dist/rsuite.min.css";
import Breaks from "./Breaks";
import { useForm, useFieldArray } from "react-hook-form";
import MyForm from "./FrontPart";
import Holidays from "./Footer";
import WeeklyHours from "./Weekly";
const SlotModal = () => {
  const [open, setOpen] = useState(false);
  const [size, setSize] = useState();
  const handleOpen = (value) => {
    clearErrors();
    setSize(value);
    setOpen(true);
  };
  const handleClose = () => setOpen(false);

  const {
    register,
    control,
  reset,
    clearErrors,
    handleSubmit,
    setError,
    watch,
    trigger,
  
    getValues,
    setValue,
    formState: { errors },
  } = useForm({  defaultValues: {
    time: [{ startime: "", endtime: "" }], // Default two entries
  }});
  const { fields, append, remove } = useFieldArray({
    control,
    name: "time",
  });
  const {
    fields: fieldhollyday,
    append: hollydayappend,
    remove: removehollyday,
  } = useFieldArray({
    control,
    name: "date",
  });

  const {
    fields: WeekFields,
    append:WeekAppend,
    remove: WeekRemove,
  } = useFieldArray({
    control,
    name: "week",
  });

  const onSubmit = async (data) => {
    console.log(data);
    console.log(getValues())
  };

  return (
    <>
      <ButtonToolbar>
        <Button size="lg" onClick={() => handleOpen("calc(90% - 80px)")}>
          Create SlotModal
        </Button>
      </ButtonToolbar>

      <Modal size={size} open={open} onClose={handleClose}>
        <Modal.Header>
          <Modal.Title>slots</Modal.Title>
        </Modal.Header>
        <Modal.Body>
          <MyForm
          className=""
            register={register}
            control={control}
            handleSubmit={handleSubmit}
            errors={errors}
            setError={setError}
            trigger={trigger}
            getValues={getValues}
            fields={fields}
            append={append}
            remove={remove}
            watch={watch}
            setValue={setValue}
          />

          <WeeklyHours
          className=""
            register={register}
            errors={errors}
            reset = {reset}
            setError={setError}
            clearErrors ={clearErrors}
            trigger={trigger}
            getValues={getValues}
            watch={watch}
            setValue={setValue}
            WeekFields={
              WeekFields.length > 0
                ? WeekFields
                : [{ startDate: null, endDate: null, name: "" }]
            }
            WeekAppend={WeekAppend}
            WeekRemove={WeekRemove}
            control={control}
          />
          <Breaks
            register={register}
            control={control}
            handleSubmit={handleSubmit}
            errors={errors}
            setError={setError}
            trigger={trigger}
            getValues={getValues}
            fields={fields}
            append={append}
            remove={remove}
            watch={watch}
            setValue={setValue}
          />
          <Holidays
            register={register}
            errors={errors}
            setError={setError}
            trigger={trigger}
            getValues={getValues}
            watch={watch}
            setValue={setValue}
            fieldhollyday={
              fieldhollyday.length > 0
                ? fieldhollyday
                : [{ startDate: null, endDate: null, name: "" }]
            }
            hollydayappend={hollydayappend}
            removehollyday={removehollyday}
            control={control}
          />
        </Modal.Body>
        <div className="d-flex justify-content-center">
          <Button onClick={handleSubmit(onSubmit)} appearance="primary">
            Prepare Slots
          </Button>
        </div>
      </Modal>
    </>
  );
};

export default SlotModal;







/* eslint-disable react/prop-types */
/* eslint-disable react/display-name */
import { useEffect, useState } from "react";
import "rsuite/dist/rsuite.min.css";
import PlusRoundIcon from "@rsuite/icons/PlusRound";
import MinusRoundIcon from "@rsuite/icons/MinusRound";
import CopyIcon from "@rsuite/icons/Copy";
import { DatePicker, Checkbox } from "rsuite";
import { forwardRef } from "react";
import { Popover, Whisper, Button, Dropdown } from "rsuite";
import { Accordion } from "rsuite";
const daysOfWeek = [
  "Sunday",
  "Monday",
  "Tuesday",
  "Wednesday",
  "Thursday",
  "Friday",
  "Saturday",
];
const MenuPopover = forwardRef(
  ({ selectedWeek, onSelect, checkedDays, setCheckedDays, ...rest }, ref) => (
    <Popover ref={ref} {...rest} full>
      <Dropdown.Menu>
        {daysOfWeek.map((day) => (
          <Dropdown.Item
            key={day}
            eventKey={day}
            onSelect={() =>
              setCheckedDays((prev) => ({ ...prev, [day]: !prev[day] }))
            }
          >
            <Checkbox
              checked={checkedDays[day] || day === selectedWeek}
              disabled={day === selectedWeek}
            >
              {day}
            </Checkbox>
          </Dropdown.Item>
        ))}
        <Dropdown.Item eventKey="apply">
          <button
            className="btn btn-primary"
            onClick={() =>
              onSelect(
                Object.keys(checkedDays).filter((day) => checkedDays[day])
              )
            }
          >
            Apply
          </button>
        </Dropdown.Item>
      </Dropdown.Menu>
    </Popover>
  )
);
const WeeklyHours = ({
  register,
  WeekAppend,
  watch,
  WeekRemove,
  WeekFields,
  errors,
  setValue,
  setError,
  clearErrors,
  trigger,
  getValues,
}) => {
  const [selectedWeek, setSelectedWeek] = useState(null);
  const [checkedDays, setCheckedDays] = useState({});
  useEffect(() => {
    WeekFields.forEach((_, index) => {
      daysOfWeek.forEach((day) => {
        register(`WeekFields[${index}].${day}.startDate`, {
          required: "Start time is required",
        });
        register(`WeekFields[${index}].${day}.endDate`, {
          required: "End time is required",
        });
        register(`WeekFields[${index}].${day}.checked`, {});
      });
    });
  }, [WeekFields, register]);

  const handleCopyClick = (day) => {
    setSelectedWeek(day);
    setCheckedDays({});
  };

 
  const handleApply = async (days) => {
    if (!days.length) return;
      const sourceIndexes = WeekFields
      .map((entry, index) => (entry[selectedWeek]?.checked ? index : -1))
      .filter(index => index !== -1);
  
    if (sourceIndexes.length === 0) {
      console.error("No valid entries found to copy.");
      return;
    }
  
    const currentValues = getValues();
    const copiedEntries = sourceIndexes.map(index => ({
      startDate: currentValues.WeekFields[index][selectedWeek]?.startDate,
      endDate: currentValues.WeekFields[index][selectedWeek]?.endDate,
    }));
    console.log("Source Indexes:", sourceIndexes);
    console.log("Copied Entries:", copiedEntries);
    if (copiedEntries.length === 0) {
      console.error("No valid entries found in source indexes.");
      return;
    }
    let newEntries = [];
    let updatedIndexes = {};
    for (const day of days) {
      let targetIndexes = WeekFields
        .map((entry, index) => (entry[day]?.checked ? index : -1))
        .filter(index => index !== -1);
      if (targetIndexes.length === 0) {
        console.log(`Adding new entries for ${day}`);
        copiedEntries.forEach((entry) => {
          newEntries.push({ [day]: { checked: true, startDate: entry.startDate, endDate: entry.endDate } });
        });
      } else {
        console.log(`Updating existing entries for ${day} at indexes:`, targetIndexes);
        targetIndexes.forEach((targetIndex,) => {
          updatedIndexes[day] = updatedIndexes[day] || [];
          updatedIndexes[day].push(targetIndex);
        });
      }
    }
    if (newEntries.length > 0) {
      WeekAppend(newEntries);
      const startIndex = WeekFields.length;
      newEntries.forEach((entry, index) => {
        const day = Object.keys(entry)[0];
        updatedIndexes[day] = updatedIndexes[day] || [];
        updatedIndexes[day].push(startIndex + index);
      });
      console.log("New entries added. Updated Indexes:", updatedIndexes);
    }
    for (const day of days) {
      if (updatedIndexes[day]) {
        updatedIndexes[day].forEach((targetIndex, i) => {
          console.log(`Final update for ${day} at index ${targetIndex}`);
  
          setValue(`WeekFields[${targetIndex}].${day}.startDate`, copiedEntries[i % copiedEntries.length].startDate, {
            shouldDirty: true,
            shouldTouch: true,
            shouldValidate: true,
          });
  
          setValue(`WeekFields[${targetIndex}].${day}.endDate`, copiedEntries[i % copiedEntries.length].endDate, {
            shouldDirty: true,
            shouldTouch: true,
            shouldValidate: true,
          });
  
          trigger(`WeekFields[${targetIndex}].${day}.startDate`);
          trigger(`WeekFields[${targetIndex}].${day}.endDate`);
        });
      }
    }
    clearErrors()
  };
  
  const handleCheckboxChange = (day) => {
    const isChecked = WeekFields.some((entry) => entry[day]?.checked);
    if (!isChecked) {
      WeekAppend({
        [day]: { checked: true, startDate: null, endDate: null },
      });
    } else {
      const index = WeekFields.findIndex((entry) => entry[day]?.checked);
      if (index !== -1) {
        WeekRemove(index);
      }
    }
  };
  const handleAppend = (day) => {
    const currentValues = getValues("WeekFields") || [];
    let allFilled = true;
    currentValues.forEach((item, index) => {
    
        if (!item.startDate) {
          allFilled = false;
          setError(`WeekFields[${index}].${day}.startDate`, {
            type: "manual",
            message: "Start time is required",
          });
        }
        if (!item.endDate) {
          allFilled = false;
          setError(`WeekFields[${index}].${day}.endDate`, {
            type: "manual",
            message: "End time is required",
          });
        }
      }
    )
    if (allFilled) {
      WeekAppend({
        [day]: { checked: true, startDate: null, endDate: null },
      });
    }
  };
  return (
    <Accordion>
      <Accordion.Panel header="Weekly Hours " defaultExpanded>
        <div className="container mt-3 card">
          <div className="card-body">
            {daysOfWeek.map((day) => (
              <div className="p-1 row" key={day}>
                <div className="d-flex align-items-center col-2 ">
                  <Checkbox
                    checked={WeekFields.some((entry) => entry[day]?.checked)}
                    onChange={() => handleCheckboxChange(day)}
                  >
                    {day}
                  </Checkbox>
                </div>
                <div className="col-6">
                  {WeekFields.some((entry) => entry[day]?.checked) ? (
                    WeekFields.map((item, index) =>
                      item[day]?.checked ? (
                        <div key={index} className="row mt-2">
                          <div className="col-md-4">
                            <label>Start time</label>
                            <DatePicker
                              format="HH:mm"
                              editable={false}
                              value={watch(
                                `WeekFields[${index}].${day}.startDate`
                              )}
                              onChange={(date) => {
                                setValue(
                                  `WeekFields[${index}].${day}.startDate`,
                                  date
                                );
                                trigger(
                                  `WeekFields[${index}].${day}.startDate`
                                );
                              }}
                            />
                            {errors.WeekFields?.[index]?.[day]?.startDate && (
                              <p className="text-danger">
                                {
                                  errors.WeekFields[index][day].startDate
                                    .message
                                }
                              </p>
                            )}
                          </div>
                          <div className="col-md-4">
                            <label>End time</label>
                            <DatePicker
                              format="HH:mm"
                              editable={false}
                              value={watch(
                                `WeekFields[${index}].${day}.endDate`
                              )}
                              onChange={(date) => {
                                setValue(
                                  `WeekFields[${index}].${day}.endDate`,
                                  date
                                );
                                trigger(`WeekFields[${index}].${day}.endDate`);
                              }}
                            />
                            {errors.WeekFields?.[index]?.[day]?.endDate && (
                              <p className="text-danger">
                                {errors.WeekFields[index][day].endDate.message}
                              </p>
                            )}
                          </div>
                          <div className="mt-3 col-2">
                            <button
                              type="button"
                              onClick={() => WeekRemove(index)}
                            >
                              <MinusRoundIcon style={{ fontSize: 15 }} />
                            </button>
                          </div>
                        </div>
                      ) : null
                    )
                  ) : (
                    <p className="pt-3">Unavailable</p>
                  )}
                </div>
                <div className="col-1 mt-3 mx-5">
                  <button type="button" onClick={() => handleAppend(day)}>
                    <PlusRoundIcon style={{ fontSize: 20 }} />
                  </button>
                </div>
                <div className="col-1 mt-3 ">
                  <Whisper
                    placement="auto"
                    trigger="click"
                    speaker={
                      <MenuPopover
                        selectedWeek={selectedWeek}
                        checkedDays={checkedDays}
                        setCheckedDays={setCheckedDays}
                        onSelect={handleApply}
                      />
                    }
                  >
                    <Button onClick={() => handleCopyClick(day)}>
                      <CopyIcon style={{ fontSize: 20, cursor: "pointer" }} />
                    </Button>
                  </Whisper>
                </div>
              </div>
            ))}
          </div>
        </div>
      </Accordion.Panel>
    </Accordion>
  );
};

export default WeeklyHours;







































..update all 





/* eslint-disable react/prop-types */
/* eslint-disable react/display-name */
import { DateTime } from "luxon";
import { useEffect, useState } from "react";
import "rsuite/dist/rsuite.min.css";
import PlusRoundIcon from "@rsuite/icons/PlusRound";
import MinusRoundIcon from "@rsuite/icons/MinusRound";
import CopyIcon from "@rsuite/icons/Copy";
import { DatePicker, Checkbox } from "rsuite";
import { forwardRef } from "react";
import { Popover, Whisper, Button, Dropdown } from "rsuite";
import { Accordion } from "rsuite";
const daysOfWeek = [
  "Sunday",
  "Monday",
  "Tuesday",
  "Wednesday",
  "Thursday",
  "Friday",
  "Saturday",
];
const MenuPopover = forwardRef(
  ({ selectedWeek, onSelect, checkedDays, setCheckedDays, ...rest }, ref) => (
    <Popover ref={ref} {...rest} full>
      <Dropdown.Menu>
        {daysOfWeek.map((day) => (
          <Dropdown.Item
            key={day}
            eventKey={day}
            onSelect={() =>
              setCheckedDays((prev) => ({ ...prev, [day]: !prev[day] }))
            }
          >
            <Checkbox
              checked={checkedDays[day] || day === selectedWeek}
              disabled={day === selectedWeek}
            >
              {day}
            </Checkbox>
          </Dropdown.Item>
        ))}
        <Dropdown.Item eventKey="apply">
          <button
            className="btn btn-primary"
            onClick={() =>
              onSelect(
                Object.keys(checkedDays).filter((day) => checkedDays[day])
              )
            }
          >
            Apply
          </button>
        </Dropdown.Item>
      </Dropdown.Menu>
    </Popover>
  )
);
const WeeklyHours = ({
  register,
  WeekAppend,
  watch,
  WeekRemove,
  WeekFields,
  errors,
  setValue,
  trigger,
  getValues,
}) => {
  const [selectedWeek, setSelectedWeek] = useState(null);
  const [checkedDays, setCheckedDays] = useState({});
  useEffect(() => {
    WeekFields.forEach((_, index) => {
      daysOfWeek.forEach((day) => {
        register(`WeekFields[${index}].${day}.startDate`, {
          required: "Start time is required",
        });
        register(`WeekFields[${index}].${day}.endDate`, {
          required: "End time is required",
        });
        register(`WeekFields[${index}].${day}.checked`, {});
      });
    });
  }, [WeekFields, register]);

  const handleCopyClick = (day) => {
    setSelectedWeek(day);
    setCheckedDays({});
  };
  // const handleApply = async (days) => {
  //   const sourceIndex = WeekFields.findIndex(
  //     (entry) => entry[selectedWeek]?.checked
  //   );
  //   console.log(sourceIndex,"sorceindexxxxxxxxxxxxxxxx")
  //   if (sourceIndex >0) return;
  //   const currentValues = getValues();
  //   console.log("Current Form Values:", currentValues);
  //   let sourceStartTime =
  //     currentValues.WeekFields?.[sourceIndex]?.[selectedWeek]?.startDate ||
  //     null;
  //   let sourceEndTime =
  //     currentValues.WeekFields?.[sourceIndex]?.[selectedWeek]?.endDate || null;

  //   console.log("Source Start Time Before Fix:", sourceStartTime);
  //   console.log("Source End Time Before Fix:", sourceEndTime);

  //   if (!sourceStartTime || !sourceEndTime) {
  //     console.error("Missing Start or End Time. Copy aborted.");
  //     return;
  //   }

  //   const getFixedTime = (date) => {
  //     return DateTime.now()
  //       .set({
  //         hour: date.hour,
  //         minute: date.minute,
  //         second: 0,
  //         millisecond: 0,
  //       })
  //       .toJSDate();
  //   };
  //   const formattedStartTime = getFixedTime(
  //     DateTime.fromJSDate(new Date(sourceStartTime))
  //   );
  //   const formattedEndTime = getFixedTime(
  //     DateTime.fromJSDate(new Date(sourceEndTime))
  //   );

  //   console.log("Formatted Start Time:", formattedStartTime);
  //   console.log("Formatted End Time:", formattedEndTime);

  //   for (let day of days) {
  //    let targetIndex =await  WeekFields.findIndex((entry) => entry[day]?.checked);

  //     if (targetIndex === -1) {
  //       console.log(`Adding new entry for ${day}`);
  //       await new Promise((resolve) => {
  //         WeekAppend({
  //           [day]: {
  //             checked: true,
  //             startDate: formattedStartTime,
  //             endDate: formattedEndTime,
  //           },
  //         });
  //         setTimeout(resolve, 100);
  //       });

  //       targetIndex = WeekFields.length;
  //     } else {
  //       console.log(
  //         `Updating existing entry for ${day} at index ${targetIndex}`
  //       );
  //     }
  //     if (!currentValues.WeekFields?.[targetIndex]?.[day]?.startDate) {
  //       await setValue(
  //         `WeekFields[${targetIndex}].${day}.startDate`,
  //         formattedStartTime,
  //         {
  //           shouldDirty: true,
  //           shouldTouch: true,
  //           shouldValidate: true,
  //         }
  //       );
  //     }
      
  //     if (!currentValues.WeekFields?.[targetIndex]?.[day]?.endDate) {
  //       await setValue(
  //         `WeekFields[${targetIndex}].${day}.endDate`,
  //         formattedEndTime,
  //         {
  //           shouldDirty: true,
  //           shouldTouch: true,
  //           shouldValidate: true,
  //         }
  //       );
  //     }

  //     trigger(`WeekFields[${targetIndex}].${day}.startDate`);
  //     trigger(`WeekFields[${targetIndex}].${day}.endDate`);

  //     console.log("Values Set for", day, "at index", targetIndex);
  //   }

  //   console.log("Copy Successful");
  // };

 
  // Function to close the popover
 
  



  const handleApply = async (days) => {
    if (!days.length) return;
  
    const sourceIndex = WeekFields.findIndex((entry) => entry[selectedWeek]?.checked);
    if (sourceIndex < 0) return; // Fix: Allow sourceIndex = 0
  
    const currentValues = getValues();
    let sourceStartTime = currentValues.WeekFields?.[sourceIndex]?.[selectedWeek]?.startDate || null;
    let sourceEndTime = currentValues.WeekFields?.[sourceIndex]?.[selectedWeek]?.endDate || null;
  
    if (!sourceStartTime || !sourceEndTime) {
      console.error("Missing Start or End Time. Copy aborted.");
      return;
    }
  
    const getFixedTime = (date) =>
      DateTime.now()
        .set({ hour: date.hour, minute: date.minute, second: 0, millisecond: 0 })
        .toJSDate();
  
    const formattedStartTime = getFixedTime(DateTime.fromJSDate(new Date(sourceStartTime)));
    const formattedEndTime = getFixedTime(DateTime.fromJSDate(new Date(sourceEndTime)));
  
    console.log("Formatted Start Time:", formattedStartTime);
    console.log("Formatted End Time:", formattedEndTime);
  
    let newEntries = [];
    let updatedIndexes = {};
  
    // First Pass: Identify missing and existing days
    for (const day of days) {
      let targetIndex = WeekFields.findIndex((entry) => entry[day]?.checked);
  
      if (targetIndex === -1) {
        console.log(`Adding new entry for ${day}`);
        newEntries.push({ [day]: { checked: true, startDate: formattedStartTime, endDate: formattedEndTime } });
      } else {
        console.log(`Updating existing entry for ${day} at index ${targetIndex}`);
        updatedIndexes[day] = targetIndex;
      }
    }
  
    // Append new entries and ensure immediate indexing
    if (newEntries.length > 0) {
      WeekAppend(newEntries);
  
      // Manually update `updatedIndexes` to prevent re-fetching delays
      const startIndex = WeekFields.length;
      newEntries.forEach((entry, index) => {
        const day = Object.keys(entry)[0];
        updatedIndexes[day] = startIndex + index; // Assign new index immediately
      });
  
      console.log("New entries added. Updated Indexes:", updatedIndexes);
    }
  
    // Second Pass: Update all days in a single click
    for (const day of days) {
      let targetIndex = updatedIndexes[day];
      if (targetIndex !== undefined) {
        console.log(`Final update for ${day} at index ${targetIndex}`);
  
        setValue(`WeekFields[${targetIndex}].${day}.startDate`, formattedStartTime, {
          shouldDirty: true,
          shouldTouch: true,
          shouldValidate: true,
        });
  
        setValue(`WeekFields[${targetIndex}].${day}.endDate`, formattedEndTime, {
          shouldDirty: true,
          shouldTouch: true,
          shouldValidate: true,
        });
  
        trigger(`WeekFields[${targetIndex}].${day}.startDate`);
        trigger(`WeekFields[${targetIndex}].${day}.endDate`);
      }
    }
  
    console.log("Copy Successful");
    closePopover(); // Auto-close popover after update
  };
  
  // Function to close the popover
  const closePopover = () => {
    // setIsPopoverOpen(false);
  };
  





  
  const handleCheckboxChange = (day) => {
    const isChecked = WeekFields.some((entry) => entry[day]?.checked);

    if (!isChecked) {
      WeekAppend({
        [day]: { checked: true, startDate: null, endDate: null },
      });
    } else {
      const index = WeekFields.findIndex((entry) => entry[day]?.checked);
      if (index !== -1) {
        WeekRemove(index);
      }
    }
  };

  const handleAppend = (day) => {
    const currentValues = getValues("WeekFields") || [];

    const exists = currentValues.some((entry) => entry[day]?.checked);

    if (!exists) {
      WeekAppend({
        [day]: { checked: true, startDate: null, endDate: null },
      });
    }
  };

  return (
    <Accordion >
      <Accordion.Panel header="Weekly Hours " defaultExpanded>
        <div className="container mt-3 card">
          <div className="card-body">
            {daysOfWeek.map((day) => (
              <div className="p-1 row" key={day}>
                <div className="d-flex align-items-center col-2 ">
                  <Checkbox
                    checked={WeekFields.some((entry) => entry[day]?.checked)}
                    onChange={() => handleCheckboxChange(day)}
                  >
                    {day}
                  </Checkbox>
                </div>
                <div className="col-6">
                  {WeekFields.some((entry) => entry[day]?.checked) ? (
                    WeekFields.map((item, index) =>
                      item[day]?.checked ? (
                        <div key={index} className="row mt-2">
                          <div className="col-md-4">
                            <label>Start time</label>
                            <DatePicker
                              format="HH:mm"
                              editable={false}
                              value={watch(
                                `WeekFields[${index}].${day}.startDate`
                              )}
                              onChange={(date) => {
                                setValue(
                                  `WeekFields[${index}].${day}.startDate`,
                                  date
                                );
                                trigger(
                                  `WeekFields[${index}].${day}.startDate`
                                );
                              }}
                            />
                            {errors.WeekFields?.[index]?.[day]?.startDate && (
                              <p className="text-danger">
                                {
                                  errors.WeekFields[index][day].startDate
                                    .message
                                }
                              </p>
                            )}
                          </div>
                          <div className="col-md-4">
                            <label>End time</label>
                            <DatePicker
                              format="HH:mm"
                              editable={false}
                              value={watch(
                                `WeekFields[${index}].${day}.endDate`
                              )}
                              onChange={(date) => {
                                setValue(
                                  `WeekFields[${index}].${day}.endDate`,
                                  date
                                );
                                trigger(`WeekFields[${index}].${day}.endDate`);
                              }}
                            />
                            {errors.WeekFields?.[index]?.[day]?.endDate && (
                              <p className="text-danger">
                                {errors.WeekFields[index][day].endDate.message}
                              </p>
                            )}
                          </div>
                          <div className="mt-3 col-2">
                            <button
                              type="button"
                              onClick={() => WeekRemove(index)}
                            >
                              <MinusRoundIcon style={{ fontSize: 15 }} />
                            </button>
                          </div>
                        </div>
                      ) : null
                    )
                  ) : (
                    <p className="pt-3">Unavailable</p>
                  )}
                </div>
                <div className="col-1 mt-3 mx-5">
                  <button type="button" onClick={() => handleAppend(day)}>
                    <PlusRoundIcon style={{ fontSize: 20 }} />
                  </button>
                </div>
                <div className="col-1 mt-3 ">
                  <Whisper
                    placement="auto"
                    trigger="click"
                    speaker={
                      <MenuPopover
                        selectedWeek={selectedWeek}
                        checkedDays={checkedDays}
                        setCheckedDays={setCheckedDays}
                        onSelect={handleApply}
                     
                      />
                    }
                  >
                    <Button onClick={() => handleCopyClick(day)}>
                      <CopyIcon style={{ fontSize: 20, cursor: "pointer" }} />
                    </Button>
                  </Whisper>
                </div>
              </div>
            ))}
          </div>
        </div>
      </Accordion.Panel>
    </Accordion>
  );
};

export default WeeklyHours;





































///////////////////////////////////////////////////////////////////////////////////////////////////////////
ALL UPDATED CODE FOR MUTLI ENTRIES AND SINGLE











/* eslint-disable react/prop-types */
/* eslint-disable react/display-name */
import { DateTime } from "luxon";
import { useEffect, useState } from "react";
import "rsuite/dist/rsuite.min.css";
import PlusRoundIcon from "@rsuite/icons/PlusRound";
import MinusRoundIcon from "@rsuite/icons/MinusRound";
import CopyIcon from "@rsuite/icons/Copy";
import { DatePicker, Checkbox } from "rsuite";
import { forwardRef } from "react";
import { Popover, Whisper, Button, Dropdown } from "rsuite";
import { Accordion } from "rsuite";
const daysOfWeek = [
  "Sunday",
  "Monday",
  "Tuesday",
  "Wednesday",
  "Thursday",
  "Friday",
  "Saturday",
];
const MenuPopover = forwardRef(
  ({ selectedWeek, onSelect, checkedDays, setCheckedDays, ...rest }, ref) => (
    <Popover ref={ref} {...rest} full>
      <Dropdown.Menu>
        {daysOfWeek.map((day) => (
          <Dropdown.Item
            key={day}
            eventKey={day}
            onSelect={() =>
              setCheckedDays((prev) => ({ ...prev, [day]: !prev[day] }))
            }
          >
            <Checkbox
              checked={checkedDays[day] || day === selectedWeek}
              disabled={day === selectedWeek}
            >
              {day}
            </Checkbox>
          </Dropdown.Item>
        ))}
        <Dropdown.Item eventKey="apply">
          <button
            className="btn btn-primary"
            onClick={() =>
              onSelect(
                Object.keys(checkedDays).filter((day) => checkedDays[day])
              )
            }
          >
            Apply
          </button>
        </Dropdown.Item>
      </Dropdown.Menu>
    </Popover>
  )
);
const WeeklyHours = ({
  register,
  WeekAppend,
  watch,
  WeekRemove,
  WeekFields,
  errors,
  setValue,
  trigger,
  getValues,
}) => {
  const [selectedWeek, setSelectedWeek] = useState(null);
  const [checkedDays, setCheckedDays] = useState({});
  useEffect(() => {
    WeekFields.forEach((_, index) => {
      daysOfWeek.forEach((day) => {
        register(`WeekFields[${index}].${day}.startDate`, {
          required: "Start time is required",
        });
        register(`WeekFields[${index}].${day}.endDate`, {
          required: "End time is required",
        });
        register(`WeekFields[${index}].${day}.checked`, {});
      });
    });
  }, [WeekFields, register]);

  const handleCopyClick = (day) => {
    setSelectedWeek(day);
    setCheckedDays({});
  };

  // const handleApply = async (days) => {
  //   if (!days.length) return;

  //   const sourceIndex = WeekFields.findIndex(
  //     (entry) => entry[selectedWeek]?.checked
  //   );
  //   if (sourceIndex < 0) return;

  //   const currentValues = getValues();
  //   let sourceStartTime =
  //     currentValues.WeekFields?.[sourceIndex]?.[selectedWeek]?.startDate ||
  //     null;
  //   let sourceEndTime =
  //     currentValues.WeekFields?.[sourceIndex]?.[selectedWeek]?.endDate || null;

  //   if (!sourceStartTime || !sourceEndTime) {
  //     console.error("Missing Start or End Time. Copy aborted.");
  //     return;
  //   }

  //   const getFixedTime = (date) =>
  //     DateTime.now()
  //       .set({
  //         hour: date.hour,
  //         minute: date.minute,
  //         second: 0,
  //         millisecond: 0,
  //       })
  //       .toJSDate();

  //   const formattedStartTime = getFixedTime(
  //     DateTime.fromJSDate(new Date(sourceStartTime))
  //   );
  //   const formattedEndTime = getFixedTime(
  //     DateTime.fromJSDate(new Date(sourceEndTime))
  //   );

  //   console.log("Formatted Start Time:", formattedStartTime);
  //   console.log("Formatted End Time:", formattedEndTime);

  //   let newEntries = [];
  //   let updatedIndexes = {};

  //   for (const day of days) {
  //     let targetIndex = WeekFields.findIndex((entry) => entry[day]?.checked);

  //     if (targetIndex === -1) {
  //       console.log(`Adding new entry for ${day}`);
  //       newEntries.push({
  //         [day]: {
  //           checked: true,
  //           startDate: formattedStartTime,
  //           endDate: formattedEndTime,
  //         },
  //       });
  //     } else {
  //       console.log(
  //         `Updating existing entry for ${day} at index ${targetIndex}`
  //       );
  //       updatedIndexes[day] = targetIndex;
  //     }
  //   }

  //   // Append new entries and ensure immediate indexing
  //   if (newEntries.length > 0) {
  //     WeekAppend(newEntries);

  //     // Manually update `updatedIndexes` to prevent re-fetching delays
  //     const startIndex = WeekFields.length;
  //     newEntries.forEach((entry, index) => {
  //       const day = Object.keys(entry)[0];
  //       updatedIndexes[day] = startIndex + index; // Assign new index immediately
  //     });

  //     console.log("New entries added. Updated Indexes:", updatedIndexes);
  //   }

  //   // Second Pass: Update all days in a single click
  //   for (const day of days) {
  //     let targetIndex = updatedIndexes[day];
  //     if (targetIndex !== undefined) {
  //       console.log(`Final update for ${day} at index ${targetIndex}`);

  //       setValue(
  //         `WeekFields[${targetIndex}].${day}.startDate`,
  //         formattedStartTime,
  //         {
  //           shouldDirty: true,
  //           shouldTouch: true,
  //           shouldValidate: true,
  //         }
  //       );

  //       setValue(
  //         `WeekFields[${targetIndex}].${day}.endDate`,
  //         formattedEndTime,
  //         {
  //           shouldDirty: true,
  //           shouldTouch: true,
  //           shouldValidate: true,
  //         }
  //       );

  //       trigger(`WeekFields[${targetIndex}].${day}.startDate`);
  //       trigger(`WeekFields[${targetIndex}].${day}.endDate`);
  //     }
  //   }

  //   console.log("Copy Successful");
  //   // closePopover(); // Auto-close popover after update
  // };
  const handleApply = async (days) => {
    if (!days.length) return;
  
    // Find all indexes where `selectedWeek` is checked
    const sourceIndexes = WeekFields
      .map((entry, index) => (entry[selectedWeek]?.checked ? index : -1))
      .filter(index => index !== -1);
  
    if (sourceIndexes.length === 0) {
      console.error("No valid entries found to copy.");
      return;
    }
  
    const currentValues = getValues();
  
    // Get all copied entries
    const copiedEntries = sourceIndexes.map(index => ({
      startDate: currentValues.WeekFields[index][selectedWeek]?.startDate,
      endDate: currentValues.WeekFields[index][selectedWeek]?.endDate,
    }));
  
    console.log("Source Indexes:", sourceIndexes);
    console.log("Copied Entries:", copiedEntries);
  
    if (copiedEntries.length === 0) {
      console.error("No valid entries found in source indexes.");
      return;
    }
  
    let newEntries = [];
    let updatedIndexes = {};
  
    for (const day of days) {
      let targetIndexes = WeekFields
        .map((entry, index) => (entry[day]?.checked ? index : -1))
        .filter(index => index !== -1);
  
      if (targetIndexes.length === 0) {
        console.log(`Adding new entries for ${day}`);
        copiedEntries.forEach((entry) => {
          newEntries.push({ [day]: { checked: true, startDate: entry.startDate, endDate: entry.endDate } });
        });
      } else {
        console.log(`Updating existing entries for ${day} at indexes:`, targetIndexes);
        targetIndexes.forEach((targetIndex,) => {
          updatedIndexes[day] = updatedIndexes[day] || [];
          updatedIndexes[day].push(targetIndex);
        });
      }
    }
  
    // Append new entries if needed
    if (newEntries.length > 0) {
      WeekAppend(newEntries);
  
      // Assign new indexes to `updatedIndexes`
      const startIndex = WeekFields.length;
      newEntries.forEach((entry, index) => {
        const day = Object.keys(entry)[0];
        updatedIndexes[day] = updatedIndexes[day] || [];
        updatedIndexes[day].push(startIndex + index);
      });
  
      console.log("New entries added. Updated Indexes:", updatedIndexes);
    }
  
    // Second Pass: Update all days in a single click
    for (const day of days) {
      if (updatedIndexes[day]) {
        updatedIndexes[day].forEach((targetIndex, i) => {
          console.log(`Final update for ${day} at index ${targetIndex}`);
  
          setValue(`WeekFields[${targetIndex}].${day}.startDate`, copiedEntries[i % copiedEntries.length].startDate, {
            shouldDirty: true,
            shouldTouch: true,
            shouldValidate: true,
          });
  
          setValue(`WeekFields[${targetIndex}].${day}.endDate`, copiedEntries[i % copiedEntries.length].endDate, {
            shouldDirty: true,
            shouldTouch: true,
            shouldValidate: true,
          });
  
          trigger(`WeekFields[${targetIndex}].${day}.startDate`);
          trigger(`WeekFields[${targetIndex}].${day}.endDate`);
        });
      }
    }
  };
  






  const handleCheckboxChange = (day) => {
    const isChecked = WeekFields.some((entry) => entry[day]?.checked);
    if (!isChecked) {
      WeekAppend({
        [day]: { checked: true, startDate: null, endDate: null },
      });
    } else {
      const index = WeekFields.findIndex((entry) => entry[day]?.checked);
      if (index !== -1) {
        WeekRemove(index);
      }
    }
  };

  const handleAppend = (day) => {
    const currentValues = getValues("WeekFields") || [];

    const exists = currentValues.some((entry) => entry[day]?.checked);

    if (!exists) {
      WeekAppend({
        [day]: { checked: true, startDate: null, endDate: null },
      });
    }
  };

  return (
    <Accordion>
      <Accordion.Panel header="Weekly Hours " defaultExpanded>
        <div className="container mt-3 card">
          <div className="card-body">
            {daysOfWeek.map((day) => (
              <div className="p-1 row" key={day}>
                <div className="d-flex align-items-center col-2 ">
                  <Checkbox
                    checked={WeekFields.some((entry) => entry[day]?.checked)}
                    onChange={() => handleCheckboxChange(day)}
                  >
                    {day}
                  </Checkbox>
                </div>
                <div className="col-6">
                  {WeekFields.some((entry) => entry[day]?.checked) ? (
                    WeekFields.map((item, index) =>
                      item[day]?.checked ? (
                        <div key={index} className="row mt-2">
                          <div className="col-md-4">
                            <label>Start time</label>
                            <DatePicker
                              format="HH:mm"
                              editable={false}
                              value={watch(
                                `WeekFields[${index}].${day}.startDate`
                              )}
                              onChange={(date) => {
                                setValue(
                                  `WeekFields[${index}].${day}.startDate`,
                                  date
                                );
                                trigger(
                                  `WeekFields[${index}].${day}.startDate`
                                );
                              }}
                            />
                            {errors.WeekFields?.[index]?.[day]?.startDate && (
                              <p className="text-danger">
                                {
                                  errors.WeekFields[index][day].startDate
                                    .message
                                }
                              </p>
                            )}
                          </div>
                          <div className="col-md-4">
                            <label>End time</label>
                            <DatePicker
                              format="HH:mm"
                              editable={false}
                              value={watch(
                                `WeekFields[${index}].${day}.endDate`
                              )}
                              onChange={(date) => {
                                setValue(
                                  `WeekFields[${index}].${day}.endDate`,
                                  date
                                );
                                trigger(`WeekFields[${index}].${day}.endDate`);
                              }}
                            />
                            {errors.WeekFields?.[index]?.[day]?.endDate && (
                              <p className="text-danger">
                                {errors.WeekFields[index][day].endDate.message}
                              </p>
                            )}
                          </div>
                          <div className="mt-3 col-2">
                            <button
                              type="button"
                              onClick={() => WeekRemove(index)}
                            >
                              <MinusRoundIcon style={{ fontSize: 15 }} />
                            </button>
                          </div>
                        </div>
                      ) : null
                    )
                  ) : (
                    <p className="pt-3">Unavailable</p>
                  )}
                </div>
                <div className="col-1 mt-3 mx-5">
                  <button type="button" onClick={() => handleAppend(day)}>
                    <PlusRoundIcon style={{ fontSize: 20 }} />
                  </button>
                </div>
                <div className="col-1 mt-3 ">
                  <Whisper
                    placement="auto"
                    trigger="click"
                    speaker={
                      <MenuPopover
                        selectedWeek={selectedWeek}
                        checkedDays={checkedDays}
                        setCheckedDays={setCheckedDays}
                        onSelect={handleApply}
                      />
                    }
                  >
                    <Button onClick={() => handleCopyClick(day)}>
                      <CopyIcon style={{ fontSize: 20, cursor: "pointer" }} />
                    </Button>
                  </Whisper>
                </div>
              </div>
            ))}
          </div>
        </div>
      </Accordion.Panel>
    </Accordion>
  );
};

export default WeeklyHours;











































import "rsuite/dist/rsuite.min.css";
import PlusRoundIcon from "@rsuite/icons/PlusRound";
import MinusRoundIcon from "@rsuite/icons/MinusRound";
import { DatePicker, Stack } from "rsuite";
import { useEffect } from "react";
import PropTypes from "prop-types";
import { Accordion } from "rsuite";

const Holidays = ({
  register,
  hollydayappend,
  removehollyday,
  fieldhollyday,
  setError,
  getValues,
  errors,
  setValue,
  trigger,
}) => {
  useEffect(() => {
    fieldhollyday.forEach((field, index) => {
      register(`date.${index}.startDate`, {
        required: "Start date is required",
      });
      register(`date.${index}.endDate`, {
        required: "End date is required",
      });
    });
  }, [fieldhollyday, register]);

  const handleAdd = () => {
    const values = getValues("date") || [];
    let allFilled = true;

    values.forEach((date, index) => {
      if (!date?.startDate) {
        allFilled = false;
        setError(`date.${index}.startDate`, {
          type: "manual",
          message: "Start date is required",
        });
      }

      if (!date?.endDate) {
        allFilled = false;
        setError(`date.${index}.endDate`, {
          type: "manual",
          message: "End date is required",
        });
      } else if (
        date.startDate &&
        date.endDate &&
        date.endDate < date.startDate
      ) {
        allFilled = false;
        setError(`date.${index}.endDate`, {
          type: "manual",
          message: "End date must be after start date",
        });
      }
    });

    if (allFilled) {
      hollydayappend({ startDate: null, endDate: null });
    }
  };

  return (
    <>
      <Accordion bordered className="my-3 ">
        <Accordion.Panel header="Holidays" defaultExpanded className="">
          <div className="container mt-3 ">
            <div className="row ">
              <div className="align-items-center mb-3 col-12">
                {fieldhollyday.map((item, index) => (
                  <div key={item.id} className="d-flex flex-row">
                    <div className="col-4 mx-1">
                      <label>Start date</label>
                      <br />
                      <Stack
                        direction="column"
                        alignItems="flex-start"
                        spacing={6}
                      >
                        <DatePicker
                          format="yyyy-MM-dd"
                          editable={false}
                          onChange={(date) => {
                            setValue(`date.${index}.startDate`, date);
                            trigger(`date.${index}.startDate`);
                          }}
                        />
                      </Stack>
                      {errors.date?.[index]?.startDate && (
                        <p className="text-danger" style={{ fontSize: "12px" }}>
                          {errors.date[index].startDate.message}
                        </p>
                      )}
                    </div>

                    <div className="col-4 mx-1">
                      <label>End date</label>
                      <br />
                      <Stack
                        direction="column"
                        alignItems="flex-start"
                        spacing={6}
                      >
                        <DatePicker
                          format="yyyy-MM-dd"
                          editable={false}
                          onChange={(date) => {
                            setValue(`date.${index}.endDate`, date);
                            trigger(`date.${index}.endDate`);
                          }}
                        />
                      </Stack>
                      {errors.date?.[index]?.endDate && (
                        <p className="text-danger" style={{ fontSize: "12px" }}>
                          {errors.date[index].endDate.message}
                        </p>
                      )}
                    </div>

                    <div>
                      <label>name</label>
                      <input className="form-control" />
                    </div>
                    <div className="col-2 ">
                      <button
                        type="button"
                        className="mt-3 mx-1 "
                        onClick={() => removehollyday(index)}
                        disabled={fieldhollyday.length === 1}
                      >
                        <MinusRoundIcon style={{ fontSize: 15 }} />
                      </button>
                      <button type="button" className="mx-1" onClick={handleAdd}>
                        <PlusRoundIcon style={{ fontSize: 15 }} />
                      </button>
                    </div>
                  </div>
                ))}
              </div>
            </div>
          </div>
        </Accordion.Panel>
      </Accordion>
      <div className="">
        <div className="">
          <label>Description</label>
          <textarea rows={2} cols={110} {...register("Description")}  className="form-control"/>
        </div>
      </div>
    </>
  );
};

Holidays.propTypes = {
  register: PropTypes.func.isRequired,
  setValue: PropTypes.func.isRequired,
  getValues: PropTypes.func.isRequired,
  errors: PropTypes.object.isRequired,
  hollydayappend: PropTypes.func.isRequired,
  removehollyday: PropTypes.func.isRequired,
  fieldhollyday: PropTypes.array.isRequired,
  setError: PropTypes.func.isRequired,
  trigger: PropTypes.func.isRequired,
};

export default Holidays;











// import { Modal, ButtonToolbar, Button } from "rsuite";
// import { useState } from "react";
// import "rsuite/dist/rsuite.min.css";
// import Breaks from "./Breaks";
// import { useForm, useFieldArray } from "react-hook-form";
// import MyForm from "./FrontPart";
// import Holidays from "./Footer";
// import WeeklyHours from "./Weekly";
// const SlotModal = () => {
//   const [open, setOpen] = useState(false);
//   const [size, setSize] = useState();
//   const handleOpen = (value) => {
//     clearErrors();
//     reset()
//     setSize(value);
//     setOpen(true);
//   };
//   const handleClose = () => setOpen(false);

//   const {
//     register,
//     control,
//   reset,
//     clearErrors,
//     handleSubmit,
//     setError,
//     watch,
//     trigger,

//     getValues,
//     setValue,
//     formState: { errors },
//   } = useForm({  defaultValues: {
//     time: [{ startime: "", endtime: "" }], // Default two entries
//   }});
//   const { fields, append, remove } = useFieldArray({
//     control,
//     name: "time",
//   });
//   const {
//     fields: fieldhollyday,
//     append: hollydayappend,
//     remove: removehollyday,
//   } = useFieldArray({
//     control,
//     name: "date",
//   });

//   const {
//     fields: WeekFields,
//     append:WeekAppend,
//     remove: WeekRemove,
//   } = useFieldArray({
//     control,
//     name: "week",
//   });

//   const onSubmit = async (data) => {
//     console.log("Form Submitted");
//   console.log("Data:", data);
//   console.log("Get Values:", getValues());
//   };

//   return (
//     <>
//       <ButtonToolbar>
//         <Button size="lg" onClick={() => handleOpen("calc(90% - 80px)")}>
//           Create SlotModal
//         </Button>
//       </ButtonToolbar>

//       <Modal size={size} open={open} onClose={handleClose}>
//         <Modal.Header>
//           <Modal.Title>slots</Modal.Title>
//         </Modal.Header>
//         <Modal.Body>
//           <MyForm
//           className=""
//             register={register}
//             control={control}
//             handleSubmit={handleSubmit}
//             errors={errors}
//             setError={setError}
//             trigger={trigger}
//             getValues={getValues}
//             fields={fields}
//             append={append}
//             remove={remove}
//             watch={watch}
//             setValue={setValue}
//           />

//           <WeeklyHours
//           className=""
//             register={register}
//             errors={errors}
//             reset = {reset}
//             setError={setError}
//             clearErrors ={clearErrors}
//             trigger={trigger}
//             getValues={getValues}
//             watch={watch}
//             setValue={setValue}
//             WeekFields={
//               WeekFields.length > 0
//                 ? WeekFields
//                 : [{ startDate: null, endDate: null, name: "" }]
//             }
//             WeekAppend={WeekAppend}
//             WeekRemove={WeekRemove}
//             control={control}
//           />
//           <Breaks
//             register={register}
//             control={control}
//             handleSubmit={handleSubmit}
//             errors={errors}
//             setError={setError}
//             trigger={trigger}
//             getValues={getValues}
//             fields={fields}
//             append={append}
//             remove={remove}
//             watch={watch}
//             setValue={setValue}
//           />
//           <Holidays
//             register={register}
//             errors={errors}
//             setError={setError}
//             trigger={trigger}
//             getValues={getValues}
//             watch={watch}
//             setValue={setValue}
//             fieldhollyday={
//               fieldhollyday.length > 0
//                 ? fieldhollyday
//                 : [{ startDate: null, endDate: null, name: "" }]
//             }
//             hollydayappend={hollydayappend}
//             removehollyday={removehollyday}
//             control={control}
//           />
//         </Modal.Body>
//         <div className="d-flex justify-content-center">
//           <Button onClick={handleSubmit(onSubmit)} appearance="primary">
//             Prepare Slots
//           </Button>
//         </div>
//       </Modal>
//     </>
//   );
// };

// export default SlotModal;




// import { DatePicker } from "rsuite";
// import "rsuite/dist/rsuite.min.css";
// import { useEffect } from "react";
// import { SelectPicker } from "rsuite";

// import PropTypes from "prop-types";
// const MyForm = ({ register, setValue, watch, errors }) => {
//   const startDate = watch("startDate"); 
//   const endDate = watch("endDate");

//   useEffect(() => {
//     register("startDate", { required: "Start date is required" });
//     register("endDate", {
//       required: "End date is required",
//       validate: (value) =>
//         value && startDate
//           ? value > startDate || "End date must be after Start date"
//           : true,
//     });
//   }, [register, startDate]);

//   return (
//     <div className="container ">
//       <div className="card-body row">
//         <div className="col-md-4">
//           <label>Time Duration</label>
//           <br />

//           <SelectPicker
//             data={[
//               { label: "10 Min", value: "10min" },
//               { label: "30 Min", value: "30min" },
//               { label: "45 Min", value: "45min" },
//             ]}
//             className="rsuite-dropdown"
//             style={{ width: 224 }}
//             placeholder="Select Duration"
//             onChange={(value) => setValue("duration", value)} 
//           />
//         </div>

//         <div className="col-md-4">
//           <label>Start Date</label>
//           <br />
//           <DatePicker
//             format="yyyy-MM-dd"
//             value={startDate || null} 
//             onChange={(date) => setValue("startDate", date)}
//             placeholder="Select Start Date"
//           />
//           {errors.startDate && (
//             <p className="text-danger" style={{ fontSize: "12px" }}>
//               {errors.startDate.message}
//             </p>
//           )}
//         </div>

//         <div className="col-md-4">
//           <label>End Date</label>
//           <br />
//           <DatePicker
//             format="yyyy-MM-dd"
//             value={endDate || null}
//             onChange={(date) => setValue("endDate", date)}
//             placeholder="Select End Date"
//           />
//           {errors.endDate && (
//             <p className="text-danger" style={{ fontSize: "12px" }}>
//               {errors.endDate.message}
//             </p>
//           )}
//         </div>
//       </div>
//     </div>
//   );
// };

// MyForm.propTypes = {
//   register: PropTypes.func.isRequired,
//   setValue: PropTypes.func.isRequired,
//   watch: PropTypes.func.isRequired,
//   errors: PropTypes.object.isRequired,
// };

// export default MyForm;






 const onSubmit = async (data) => {
    console.log(" Validating form...");
    const isValid = await trigger(); // Validate the entire form
    console.log(getValues());
    if (!isValid) {
      console.error(" Validation failed.");
      return;
    }

    console.log(" Form Submitted Successfully!");
    setOpen(false);
    console.log(" Data:", data);
  };

























































/* eslint-disable react/prop-types */
/* eslint-disable react/display-name */
// import { DateTime } from "luxon";
import { useEffect, useState } from "react";
import "rsuite/dist/rsuite.min.css";
import PlusRoundIcon from "@rsuite/icons/PlusRound";
import MinusRoundIcon from "@rsuite/icons/MinusRound";
import CopyIcon from "@rsuite/icons/Copy";
import { DatePicker, Checkbox } from "rsuite";
import { forwardRef } from "react";
import { Popover, Whisper, Button, Dropdown } from "rsuite";
import { Accordion } from "rsuite";
const daysOfWeek = [
  "Sunday",
  "Monday",
  "Tuesday",
  "Wednesday",
  "Thursday",
  "Friday",
  "Saturday",
];
const MenuPopover = forwardRef(
  ({ selectedWeek, onSelect, checkedDays, setCheckedDays, ...rest }, ref) => (
    <Popover ref={ref} {...rest} full>
      <Dropdown.Menu>
        {daysOfWeek.map((day) => (
          <Dropdown.Item
            key={day}
            eventKey={day}
            onSelect={() =>
              setCheckedDays((prev) => ({ ...prev, [day]: !prev[day] }))
            }
          >
            <Checkbox
              checked={checkedDays[day] || day === selectedWeek}
              disabled={day === selectedWeek}
            >
              {day}
            </Checkbox>
          </Dropdown.Item>
        ))}
        <Dropdown.Item eventKey="apply">
          <button
            className="btn btn-primary"
            onClick={() =>
              onSelect(
                Object.keys(checkedDays).filter((day) => checkedDays[day])
              )
            }
          >
            Apply
          </button>
        </Dropdown.Item>
      </Dropdown.Menu>
    </Popover>
  )
);
const WeeklyHours = ({
  register,
  WeekAppend,
  watch,
  WeekRemove,
  WeekFields,
  errors,
  setError,
  setValue,
  trigger,
  getValues,
}) => {
  const [selectedWeek, setSelectedWeek] = useState(null);
  const [checkedDays, setCheckedDays] = useState({});
  useEffect(() => {
    WeekFields.forEach((_, index) => {
      daysOfWeek.forEach((day) => {
        register(`WeekFields[${index}].${day}.startDate`, {
          required: "Start time is required",
        });
        register(`WeekFields[${index}].${day}.endDate`, {
          required: "End time is required",
        });
        register(`WeekFields[${index}].${day}.checked`, {});
      });
    });
  }, [WeekFields, register]);

  const handleCopyClick = (day) => {
    setSelectedWeek(day);
    setCheckedDays({});
  };

  // const handleApply = async (days) => {
  //   if (!days.length) return;

  //   const sourceIndex = WeekFields.findIndex(
  //     (entry) => entry[selectedWeek]?.checked
  //   );
  //   if (sourceIndex < 0) return;

  //   const currentValues = getValues();
  //   let sourceStartTime =
  //     currentValues.WeekFields?.[sourceIndex]?.[selectedWeek]?.startDate ||
  //     null;
  //   let sourceEndTime =
  //     currentValues.WeekFields?.[sourceIndex]?.[selectedWeek]?.endDate || null;

  //   if (!sourceStartTime || !sourceEndTime) {
  //     console.error("Missing Start or End Time. Copy aborted.");
  //     return;
  //   }

  //   const getFixedTime = (date) =>
  //     DateTime.now()
  //       .set({
  //         hour: date.hour,
  //         minute: date.minute,
  //         second: 0,
  //         millisecond: 0,
  //       })
  //       .toJSDate();

  //   const formattedStartTime = getFixedTime(
  //     DateTime.fromJSDate(new Date(sourceStartTime))
  //   );
  //   const formattedEndTime = getFixedTime(
  //     DateTime.fromJSDate(new Date(sourceEndTime))
  //   );

  //   console.log("Formatted Start Time:", formattedStartTime);
  //   console.log("Formatted End Time:", formattedEndTime);

  //   let newEntries = [];
  //   let updatedIndexes = {};

  //   for (const day of days) {
  //     let targetIndex = WeekFields.findIndex((entry) => entry[day]?.checked);

  //     if (targetIndex === -1) {
  //       console.log(`Adding new entry for ${day}`);
  //       newEntries.push({
  //         [day]: {
  //           checked: true,
  //           startDate: formattedStartTime,
  //           endDate: formattedEndTime,
  //         },
  //       });
  //     } else {
  //       console.log(
  //         `Updating existing entry for ${day} at index ${targetIndex}`
  //       );
  //       updatedIndexes[day] = targetIndex;
  //     }
  //   }

  //   // Append new entries and ensure immediate indexing
  //   if (newEntries.length > 0) {
  //     WeekAppend(newEntries);

  //     // Manually update `updatedIndexes` to prevent re-fetching delays
  //     const startIndex = WeekFields.length;
  //     newEntries.forEach((entry, index) => {
  //       const day = Object.keys(entry)[0];
  //       updatedIndexes[day] = startIndex + index; // Assign new index immediately
  //     });

  //     console.log("New entries added. Updated Indexes:", updatedIndexes);
  //   }

  //   // Second Pass: Update all days in a single click
  //   for (const day of days) {
  //     let targetIndex = updatedIndexes[day];
  //     if (targetIndex !== undefined) {
  //       console.log(`Final update for ${day} at index ${targetIndex}`);

  //       setValue(
  //         `WeekFields[${targetIndex}].${day}.startDate`,
  //         formattedStartTime,
  //         {
  //           shouldDirty: true,
  //           shouldTouch: true,
  //           shouldValidate: true,
  //         }
  //       );

  //       setValue(
  //         `WeekFields[${targetIndex}].${day}.endDate`,
  //         formattedEndTime,
  //         {
  //           shouldDirty: true,
  //           shouldTouch: true,
  //           shouldValidate: true,
  //         }
  //       );

  //       trigger(`WeekFields[${targetIndex}].${day}.startDate`);
  //       trigger(`WeekFields[${targetIndex}].${day}.endDate`);
  //     }
  //   }

  //   console.log("Copy Successful");
  //   // closePopover(); // Auto-close popover after update
  // };
  const handleApply = async (days) => {
    if (!days.length) return;
  
    // Find all indexes where `selectedWeek` is checked
    const sourceIndexes = WeekFields
      .map((entry, index) => (entry[selectedWeek]?.checked ? index : -1))
      .filter(index => index !== -1);
  
    if (sourceIndexes.length === 0) {
      console.error("No valid entries found to copy.");
      return;
    }
  
    const currentValues = getValues();
  
    // Get all copied entries
    const copiedEntries = sourceIndexes.map(index => ({
      startDate: currentValues.WeekFields[index][selectedWeek]?.startDate,
      endDate: currentValues.WeekFields[index][selectedWeek]?.endDate,
    }));
  
    console.log("Source Indexes:", sourceIndexes);
    console.log("Copied Entries:", copiedEntries);
  
    if (copiedEntries.length === 0) {
      console.error("No valid entries found in source indexes.");
      return;
    }
  
    let newEntries = [];
    let updatedIndexes = {};
  
    for (const day of days) {
      let targetIndexes = WeekFields
        .map((entry, index) => (entry[day]?.checked ? index : -1))
        .filter(index => index !== -1);
  
      if (targetIndexes.length === 0) {
        console.log(`Adding new entries for ${day}`);
        copiedEntries.forEach((entry) => {
          newEntries.push({ [day]: { checked: true, startDate: entry.startDate, endDate: entry.endDate } });
        });
      } else {
        console.log(`Updating existing entries for ${day} at indexes:`, targetIndexes);
        targetIndexes.forEach((targetIndex,) => {
          updatedIndexes[day] = updatedIndexes[day] || [];
          updatedIndexes[day].push(targetIndex);
        });
      }
    }
  
    // Append new entries if needed
    if (newEntries.length > 0) {
      WeekAppend(newEntries);
  
      // Assign new indexes to `updatedIndexes`
      const startIndex = WeekFields.length;
      newEntries.forEach((entry, index) => {
        const day = Object.keys(entry)[0];
        updatedIndexes[day] = updatedIndexes[day] || [];
        updatedIndexes[day].push(startIndex + index);
      });
  
      console.log("New entries added. Updated Indexes:", updatedIndexes);
    }
  
    // Second Pass: Update all days in a single click
    for (const day of days) {
      if (updatedIndexes[day]) {
        updatedIndexes[day].forEach((targetIndex, i) => {
          console.log(`Final update for ${day} at index ${targetIndex}`);
  
          setValue(`WeekFields[${targetIndex}].${day}.startDate`, copiedEntries[i % copiedEntries.length].startDate, {
            shouldDirty: true,
            shouldTouch: true,
            shouldValidate: true,
          });
  
          setValue(`WeekFields[${targetIndex}].${day}.endDate`, copiedEntries[i % copiedEntries.length].endDate, {
            shouldDirty: true,
            shouldTouch: true,
            shouldValidate: true,
          });
  
          trigger(`WeekFields[${targetIndex}].${day}.startDate`);
          trigger(`WeekFields[${targetIndex}].${day}.endDate`);
        });
      }
    }
  };
  






  const handleCheckboxChange = (day) => {
    const isChecked = WeekFields.some((entry) => entry[day]?.checked);
    if (!isChecked) {
      WeekAppend({
        [day]: { checked: true, startDate: null, endDate: null },
      });
    } else {
      const index = WeekFields.findIndex((entry) => entry[day]?.checked);
      if (index !== -1) {
        WeekRemove(index);
      }
    }
  };

  // const handleAppend = () => {
  //   const values = getValues("time") || [];
  //   let allFilled = true;

  //   values.forEach((time, index) => {
  //     if (!time.startime) {
  //       allFilled = false;
  //       setError(`time[${index}].startime`, {
  //         type: "manual",
  //         message: "Start time is required",
  //       });
  //     }

  //     if (!time.endtime) {
  //       allFilled = false;
  //       setError(`time[${index}].endtime`, {
  //         type: "manual",
  //         message: "End time is required",
  //       });
  //     }
  //   });

  //   if (allFilled) {
  //     WeekAppend({ startime: null, endtime: null });
  //   }
  // };
  
  const handleAppend = (day) => {
    const currentValues = getValues("WeekFields");
    // let allFilled = true;
    currentValues.forEach((item, index) => {
      if (!item[day]?.startDate) {
        // allFilled = false;
        setError(`WeekFields[${index}].${day}.startDate`, {
          type: "manual",
          message: "Start time is required",
        });
      }
      if (!item[day]?.endDate) {
        // allFilled =false;
        setError(`WeekFields[${index}].${day}.endDate`, {
          type: "manual",
          message: "End time is required",
        });
      } else {
        WeekAppend({
          [day]: { checked: true, startDate: null, endDate: null },
        });
        // clearErrors();
      }
    });
  };
  return (
    <Accordion>
      <Accordion.Panel header="Weekly Hours " defaultExpanded>
        <div className="container mt-3 card">
          <div className="card-body">
            {daysOfWeek.map((day) => (
              <div className="p-1 row" key={day}>
                <div className="d-flex align-items-center col-2 ">
                  <Checkbox
                    checked={WeekFields.some((entry) => entry[day]?.checked)}
                    onChange={() => handleCheckboxChange(day)}
                  >
                    {day}
                  </Checkbox>
                </div>
                <div className="col-6">
                  {WeekFields.some((entry) => entry[day]?.checked) ? (
                    WeekFields.map((item, index) =>
                      item[day]?.checked ? (
                        <div key={index} className="row mt-2">
                          <div className="col-md-4">
                            <label>Start time</label>
                            <DatePicker
                              format="HH:mm"
                              editable={false}
                              value={watch(
                                `WeekFields[${index}].${day}.startDate`
                              )}
                              onChange={(date) => {
                                setValue(
                                  `WeekFields[${index}].${day}.startDate`,
                                  date
                                );
                                trigger(
                                  `WeekFields[${index}].${day}.startDate`
                                );
                              }}
                            />
                            {errors.WeekFields?.[index]?.[day]?.startDate && (
                              <p className="text-danger">
                                {
                                  errors.WeekFields[index][day].startDate
                                    .message
                                }
                              </p>
                            )}
                          </div>
                          <div className="col-md-4">
                            <label>End time</label>
                            <DatePicker
                              format="HH:mm"
                              editable={false}
                              value={watch(
                                `WeekFields[${index}].${day}.endDate`
                              )}
                              onChange={(date) => {
                                setValue(
                                  `WeekFields[${index}].${day}.endDate`,
                                  date
                                );
                                trigger(`WeekFields[${index}].${day}.endDate`);
                              }}
                            />
                            {errors.WeekFields?.[index]?.[day]?.endDate && (
                              <p className="text-danger">
                                {errors.WeekFields[index][day].endDate.message}
                              </p>
                            )}
                          </div>
                          <div className="mt-3 col-2">
                            <button
                              type="button"
                              onClick={() => WeekRemove(index)}
                            >
                              <MinusRoundIcon style={{ fontSize: 15 }} />
                            </button>
                          </div>
                        </div>
                      ) : null
                    )
                  ) : (
                    <p className="pt-3">Unavailable</p>
                  )}
                </div>
                <div className="col-1 mt-3 mx-5">
                  <button type="button" onClick={() => handleAppend(day)}>
                    <PlusRoundIcon style={{ fontSize: 20 }} />
                  </button>
                </div>
                <div className="col-1 mt-3 ">
                  <Whisper
                    placement="auto"
                    trigger="click"
                    speaker={
                      <MenuPopover
                        selectedWeek={selectedWeek}
                        checkedDays={checkedDays}
                        setCheckedDays={setCheckedDays}
                        onSelect={handleApply}
                      />
                    }
                  >
                    <Button onClick={() => handleCopyClick(day)}>
                      <CopyIcon style={{ fontSize: 20, cursor: "pointer" }} />
                    </Button>
                  </Whisper>
                </div>
              </div>
            ))}
          </div>
        </div>
      </Accordion.Panel>
    </Accordion>
  );
};

export default WeeklyHours;
  
















  /* eslint-disable react/prop-types */
/* eslint-disable react/display-name */

import { useEffect, useState } from "react";
import "rsuite/dist/rsuite.min.css";
import PlusRoundIcon from "@rsuite/icons/PlusRound";
import MinusRoundIcon from "@rsuite/icons/MinusRound";
import CopyIcon from "@rsuite/icons/Copy";
import { DatePicker, Checkbox } from "rsuite";
import { forwardRef } from "react";
import { Popover, Whisper, Button, Dropdown } from "rsuite";
import { Accordion } from "rsuite";

const daysOfWeek = [
  "Sunday",
  "Monday",
  "Tuesday",
  "Wednesday",
  "Thursday",
  "Friday",
  "Saturday",
];

const MenuPopover = forwardRef(
  ({ selectedWeek, onSelect, checkedDays, setCheckedDays, ...rest }, ref) => (
    <Popover ref={ref} {...rest} full>
      <Dropdown.Menu>
        {daysOfWeek.map((day) => (
          <Dropdown.Item
            key={day}
            eventKey={day}
            onSelect={() =>
              setCheckedDays((prev) => ({ ...prev, [day]: !prev[day] }))
            }
          >
            <Checkbox
              checked={checkedDays[day] || day === selectedWeek}
              disabled={day === selectedWeek}
            >
              {day}
            </Checkbox>
          </Dropdown.Item>
        ))}
        <Dropdown.Item eventKey="apply">
          <button
            className="btn btn-primary"
            onClick={() =>
              onSelect(
                Object.keys(checkedDays).filter((day) => checkedDays[day])
              )
            }
          >
            Apply
          </button>
        </Dropdown.Item>
      </Dropdown.Menu>
    </Popover>
  )
);

const WeeklyHours = ({
  register,
  WeekAppend,
  watch,
  WeekRemove,
  WeekFields,
  errors,
  setValue,
  setError,
  clearErrors,
  trigger,
  getValues,
}) => {
  const [selectedWeek, setSelectedWeek] = useState(null);
  const [checkedDays, setCheckedDays] = useState({});

  useEffect(() => {
    WeekFields.forEach((_, index) => {
      daysOfWeek.forEach((day) => {
        register(`week[${index}].${day}.startDate`);
        register(`week[${index}].${day}.endDate`);
        register(`week[${index}].${day}.checked`);
      });
    });
  }, [WeekFields, register]);

  const handleCopyClick = (day) => {
    setSelectedWeek(day);
    setCheckedDays({});
  };

  const handleApply = async (days) => {
    if (!days.length) return;
    const sourceIndexes = WeekFields.map((entry, index) =>
      entry[selectedWeek]?.checked ? index : -1
    ).filter((index) => index !== -1);

    if (sourceIndexes.length === 0) {
      return;
    }

    const currentValues = getValues();
    const copiedEntries = sourceIndexes.map((index) => ({
      startDate: currentValues.WeekFields[index][selectedWeek]?.startDate,
      endDate: currentValues.WeekFields[index][selectedWeek]?.endDate,
    }));

    if (copiedEntries.length === 0) {
      console.error("No valid entries found in source indexes.");
      return;
    }
    let newEntries = [];
    let updatedIndexes = {};
    for (const day of days) {
      let targetIndexes = WeekFields.map((entry, index) =>
        entry[day]?.checked ? index : -1
      ).filter((index) => index !== -1);

      if (targetIndexes.length === 0) {
        copiedEntries.forEach((entry) => {
          newEntries.push({
            [day]: {
              checked: true,
              startDate: entry.startDate,
              endDate: entry.endDate,
            },
          });
        });
      } else {
        targetIndexes.forEach((targetIndex) => {
          updatedIndexes[day] = updatedIndexes[day] || [];
          updatedIndexes[day].push(targetIndex);
        });
      }
    }
    if (newEntries.length > 0) {
      WeekAppend(newEntries);
      const startIndex = WeekFields.length;
      newEntries.forEach((entry, index) => {
        const day = Object.keys(entry)[0];
        updatedIndexes[day] = updatedIndexes[day] || [];
        updatedIndexes[day].push(startIndex + index);
      });
    }
    for (const day of days) {
      if (updatedIndexes[day]) {
        updatedIndexes[day].forEach((targetIndex, i) => {
          setValue(
            `WeekFields[${targetIndex}].${day}.startDate`,
            copiedEntries[i % copiedEntries.length].startDate
          );
          trigger(`WeekFields[${targetIndex}].${day}.startDate`);

          setValue(
            `WeekFields[${targetIndex}].${day}.endDate`,
            copiedEntries[i % copiedEntries.length].endDate,
            {
              shouldDirty: true,
              shouldTouch: true,
              shouldValidate: true,
            }
          );

          trigger(`WeekFields[${targetIndex}].${day}.endDate`);
        });
      }
    }
    await trigger();
    clearErrors();
  };

  const handleCheckboxChange = (day) => {
    const isChecked = WeekFields.some((entry) => entry[day]?.checked);
    if (!isChecked) {
      WeekAppend({
        [day]: { checked: true, startDate: null, endDate: null },
      });
      const newIndex = WeekFields.length;
      register(`WeekFields[${newIndex}].${day}.startDate`);
      register(`WeekFields[${newIndex}].${day}.endDate`);
      register(`WeekFields[${newIndex}].${day}.checked`);
    } else {
      const index = WeekFields.findIndex((entry) => entry[day]?.checked);
      if (index !== -1) {
        WeekRemove(index);
      }
    }
  };

  const handleAppend = (day) => {
    const currentValues = getValues("WeekFields");
    currentValues.forEach((item, index) => {
      if (!item[day]?.startDate) {
        setError(`WeekFields[${index}].${day}.startDate`, {
          type: "manual",
          message: "Start time is required",
        });
      }
      if (!item[day]?.endDate) {
        setError(`WeekFields[${index}].${day}.endDate`, {
          type: "manual",
          message: "End time is required",
        });
      }
    });

    // Append new field
    WeekAppend({
      [day]: { checked: true, startDate: null, endDate: null },
    });

    // Register the new field
    const newIndex = WeekFields.length;
    register(`WeekFields[${newIndex}].${day}.startDate`);
    register(`WeekFields[${newIndex}].${day}.endDate`);
    register(`WeekFields[${newIndex}].${day}.checked`);

    console.log(`New field appended for ${day}`);
  };

  return (
    <Accordion>
      <Accordion.Panel header="Weekly Hours " defaultExpanded>
        <div className="container mt-3 card">
          <div className="card-body">
            {daysOfWeek.map((day) => (
              <div className="p-1 row" key={day}>
                <div className="d-flex align-items-center col-2 ">
                  <Checkbox
                    checked={WeekFields.some((entry) => entry[day]?.checked)}
                    onChange={() => handleCheckboxChange(day)}
                  >
                    {day}
                  </Checkbox>
                </div>
                <div className="col-6">
                  {WeekFields.some((entry) => entry[day]?.checked) ? (
                    WeekFields.map((item, index) =>
                      item[day]?.checked ? (
                        <div key={index} className="row mt-2">
                          <div className="col-md-4">
                            <label>Start time</label>
                            <DatePicker
                              format="HH:mm"
                              editable={false}
                              value={watch(
                                `WeekFields[${index}].${day}.startDate`
                              )}
                              onChange={(date) => {
                                setValue(
                                  `WeekFields[${index}].${day}.startDate`,
                                  date
                                );
                                trigger(
                                  `WeekFields[${index}].${day}.startDate`
                                );
                              }}
                            />
                            {errors.WeekFields?.[index]?.[day]?.startDate && (
                              <p className="text-danger">
                                {
                                  errors.WeekFields[index][day].startDate
                                    .message
                                }
                              </p>
                            )}
                          </div>
                          <div className="col-md-4">
                            <label>End time</label>
                            <DatePicker
                              format="HH:mm"
                              editable={false}
                              value={watch(
                                `WeekFields[${index}].${day}.endDate`
                              )}
                              onChange={(date) => {
                                setValue(
                                  `WeekFields[${index}].${day}.endDate`,
                                  date
                                );
                                trigger(`WeekFields[${index}].${day}.endDate`);
                              }}
                            />
                            {errors.WeekFields?.[index]?.[day]?.endDate && (
                              <p className="text-danger">
                                {errors.WeekFields[index][day].endDate.message}
                              </p>
                            )}
                          </div>
                          <div className="mt-3 col-2">
                            <button
                              type="button"
                              onClick={() => WeekRemove(index)}
                            >
                              <MinusRoundIcon style={{ fontSize: 15 }} />
                            </button>
                          </div>
                        </div>
                      ) : null
                    )
                  ) : (
                    <p className="pt-3">Unavailable</p>
                  )}
                </div>
                <div className="col-1 mt-3 mx-5">
                  <button type="button" onClick={() => handleAppend(day)}>
                    <PlusRoundIcon style={{ fontSize: 20 }} />
                  </button>
                </div>
                <div className="col-1 mt-3 ">
                  <Whisper
                    placement="auto"
                    trigger="click"
                    speaker={
                      <MenuPopover
                        selectedWeek={selectedWeek}
                        checkedDays={checkedDays}
                        setCheckedDays={setCheckedDays}
                        onSelect={handleApply}
                      />
                    }
                  >
                    <Button onClick={() => handleCopyClick(day)}>
                      <CopyIcon style={{ fontSize: 20, cursor: "pointer" }} />
                    </Button>
                  </Whisper>
                </div>
              </div>
            ))}
          </div>
        </div>
      </Accordion.Panel>
    </Accordion>
  );
};

export default WeeklyHours;



























/* eslint-disable react/prop-types */
/* eslint-disable react/display-name */



import { useEffect, useState } from "react";
import "rsuite/dist/rsuite.min.css";
import PlusRoundIcon from "@rsuite/icons/PlusRound";
import MinusRoundIcon from "@rsuite/icons/MinusRound";
import CopyIcon from "@rsuite/icons/Copy";
import { DatePicker, Checkbox } from "rsuite";
import { forwardRef } from "react";
import { Popover, Whisper, Button, Dropdown } from "rsuite";
import { Accordion } from "rsuite";

const daysOfWeek = [
  "Sunday",
  "Monday",
  "Tuesday",
  "Wednesday",
  "Thursday",
  "Friday",
  "Saturday",
];

const MenuPopover = forwardRef(
  ({ selectedWeek, onSelect, checkedDays, setCheckedDays,onClose ,...rest }, ref) => (
    <Popover ref={ref} {...rest} full>
      <Dropdown.Menu>
        {daysOfWeek.map((day) => (
          <Dropdown.Item
            key={day}
            eventKey={day}
            onSelect={() =>
              setCheckedDays((prev) => ({ ...prev, [day]: !prev[day] }))
            }
          >
            <Checkbox
              checked={checkedDays[day] || day === selectedWeek}
              disabled={day === selectedWeek}
            >
              {day}
            </Checkbox>
          </Dropdown.Item>
        ))}
        <Dropdown.Item eventKey="apply">
        <button className="btn btn-primary" onClick={() => { onSelect(Object.keys(checkedDays).filter((day) => checkedDays[day])); onClose(); }}>
        Apply
          </button>
        </Dropdown.Item>
      </Dropdown.Menu>
    </Popover>
  )
);

const WeeklyHours = ({
  register,
  WeekAppend,
  watch,
  WeekRemove,
  WeekFields,
  errors,
  setValue,
  setError,
  clearErrors,
  trigger,
  getValues,
}) => {
  const [selectedWeek, setSelectedWeek] = useState(null);
  const [checkedDays, setCheckedDays] = useState({});

  useEffect(() => {
    WeekFields.forEach((_, index) => {
      daysOfWeek.forEach((day) => {
        register(`week[${index}].${day}.startDate`);
        register(`week[${index}].${day}.endDate`);
        register(`week[${index}].${day}.checked`);
      });
    });
  }, [WeekFields, register]);

  const handleCopyClick = (day) => {
    setSelectedWeek(day);
    setCheckedDays({});
  };

  const handleApply = async (days) => {
    if (!days.length) return;
    const sourceIndexes = WeekFields.map((entry, index) =>
      entry[selectedWeek]?.checked ? index : -1
    ).filter((index) => index !== -1);

    if (sourceIndexes.length === 0) {
      return;
    }

    const currentValues = getValues();
    const copiedEntries = sourceIndexes.map((index) => ({
      startDate: currentValues.WeekFields[index][selectedWeek]?.startDate,
      endDate: currentValues.WeekFields[index][selectedWeek]?.endDate,
    }));

    if (copiedEntries.length === 0) {
      console.error("No valid entries found in source indexes.");
      return;
    }
    let newEntries = [];
    let updatedIndexes = {};
    for (const day of days) {
      let targetIndexes = WeekFields.map((entry, index) =>
        entry[day]?.checked ? index : -1
      ).filter((index) => index !== -1);

      if (targetIndexes.length === 0) {
        copiedEntries.forEach((entry) => {
          newEntries.push({
            [day]: {
              checked: true,
              startDate: entry.startDate,
              endDate: entry.endDate,
            },
          });
        });
      } else {
        targetIndexes.forEach((targetIndex) => {
          updatedIndexes[day] = updatedIndexes[day] || [];
          updatedIndexes[day].push(targetIndex);
        });
      }
    }
    if (newEntries.length > 0) {
      WeekAppend(newEntries);
      const startIndex = WeekFields.length;
      newEntries.forEach((entry, index) => {
        const day = Object.keys(entry)[0];
        updatedIndexes[day] = updatedIndexes[day] || [];
        updatedIndexes[day].push(startIndex + index);
      });
    }
    for (const day of days) {
      if (updatedIndexes[day]) {
        updatedIndexes[day].forEach((targetIndex, i) => {
          setValue(
            `WeekFields[${targetIndex}].${day}.startDate`,
            copiedEntries[i % copiedEntries.length].startDate
          );
          trigger(`WeekFields[${targetIndex}].${day}.startDate`);

          setValue(
            `WeekFields[${targetIndex}].${day}.endDate`,
            copiedEntries[i % copiedEntries.length].endDate,
            {
              shouldDirty: true,
              shouldTouch: true,
              shouldValidate: true,
            }
          );

          trigger(`WeekFields[${targetIndex}].${day}.endDate`);
        });
      }
    }
    await trigger();
    clearErrors();
  };

  const handleCheckboxChange = (day) => {
    const isChecked = WeekFields.some((entry) => entry[day]?.checked);
    if (!isChecked) {
      WeekAppend({
        [day]: { checked: true, startDate: null, endDate: null },
      });
      const newIndex = WeekFields.length;
      register(`WeekFields[${newIndex}].${day}.startDate`);
      register(`WeekFields[${newIndex}].${day}.endDate`);
      register(`WeekFields[${newIndex}].${day}.checked`);
    } else {
      const index = WeekFields.findIndex((entry) => entry[day]?.checked);
      if (index !== -1) {
        WeekRemove(index);
      }
    }
  };
  // const handleAppend = (day) => {
  //   const currentValues = getValues("WeekFields");
  //   let allFieldsFilled = true;
   
  //   currentValues.forEach((item, index) => {
  //     if (!item[day]?.startDate) {
  //       setError(`WeekFields[${index}].${day}.startDate`, {
  //         type: "manual",
  //         message: "Start time is required",
  //       });
  //       allFieldsFilled = false; 
  //     }
  //     if (!item[day]?.endDate) {
  //       setError(`WeekFields[${index}].${day}.endDate`, {
  //         type: "manual",
  //         message: "End time is required",
  //       });
  //       allFieldsFilled = false;
  //     }
  //   });
  
    
  //   if (!allFieldsFilled) {
  //     WeekAppend(
  //        { checked: true, startDate: "", endDate: "" },
  //     );
  
  //       const updatedValues = getValues("WeekFields"); 
  //       const newIndex = updatedValues.length - 1; 
  
  //       register(`WeekFields[${newIndex}].${day}.startDate`);
  //       register(`WeekFields[${newIndex}].${day}.endDate`);
  //       register(`WeekFields[${newIndex}].${day}.checked`);
  
  //       console.log(`New field appended for ${day} at index ${newIndex}`);

  //   } else {
  //     console.log("Cannot append, fill all fields first.");
  //   }
  // };
  
  const handleAppend = (day) => {
    const currentValues = getValues("WeekFields") || []; 
    let allFieldsFilled = true;
  
    currentValues.forEach((item, index) => {
      if (!item[day]?.startDate) {
        setError(`WeekFields[${index}].${day}.startDate`, {
          type: "manual",
          message: "Start time is required",
        });
        allFieldsFilled = false;
      }
      if (!item[day]?.endDate) {
        setError(`WeekFields[${index}].${day}.endDate`, {
          type: "manual",
          message: "End time is required",
        });
        allFieldsFilled = false;
      }
    });
  

    if (allFieldsFilled) {
      WeekAppend({
        [day]: {
          checked: true,
          startDate: "",
          endDate: "",
        },
      });
  
      console.log(`New field appended for ${day}`);
    } else {
      console.log("Cannot append, fill all fields first.");
    }
  };

  return (
    <Accordion>
      <Accordion.Panel header="Weekly Hours " defaultExpanded>
        <div className="container mt-3 card">
          <div className="card-body">
            {daysOfWeek.map((day) => (
              <div className="p-1 row" key={day}>
                <div className="d-flex align-items-center col-2 ">
                  <Checkbox
                    checked={WeekFields.some((entry) => entry[day]?.checked)}
                    onChange={() => handleCheckboxChange(day)}
                  >
                    {day}
                  </Checkbox>
                </div>
                <div className="col-6">
                  {WeekFields.some((entry) => entry[day]?.checked) ? (
                    WeekFields.map((item, index) =>
                      item[day]?.checked ? (
                        <div key={index} className="row mt-2">
                          <div className="col-md-4">
                            <label>Start time</label>
                            <DatePicker
                              format="HH:mm"
                              editable={false}
                              value={watch(
                                `WeekFields[${index}].${day}.startDate`
                              )}
                              onChange={(date) => {
                                setValue(
                                  `WeekFields[${index}].${day}.startDate`,
                                  date
                                );
                                trigger(
                                  `WeekFields[${index}].${day}.startDate`
                                );
                              }}
                            />
                            {errors.WeekFields?.[index]?.[day]?.startDate && (
                              <p className="text-danger">
                                {
                                  errors.WeekFields[index][day].startDate
                                    .message
                                }
                              </p>
                            )}
                          </div>
                          <div className="col-md-4">
                            <label>End time</label>
                            <DatePicker
                              format="HH:mm"
                              editable={false}
                              value={watch(
                                `WeekFields[${index}].${day}.endDate`
                              )}
                              onChange={(date) => {
                                setValue(
                                  `WeekFields[${index}].${day}.endDate`,
                                  date
                                );
                                trigger(`WeekFields[${index}].${day}.endDate`);
                              }}
                            />
                            {errors.WeekFields?.[index]?.[day]?.endDate && (
                              <p className="text-danger">
                            {errors.WeekFields[index][day].endDate.message}
                              </p>
                            )}
                          </div>
                          <div className="mt-3 col-2">
                            <button
                              type="button"
                              onClick={() => WeekRemove(index)}
                            >
                              <MinusRoundIcon style={{ fontSize: 15 }} />
                            </button>
                          </div>
                        </div>
                      ) : null
                    )
                  ) : (
                    <p className="pt-3">Unavailable</p>
                  )}
                </div>
                <div className="col-1 mt-3 mx-5">
                  <button type="button" onClick={() => handleAppend(day)}>
                    <PlusRoundIcon style={{ fontSize: 20 }} />
                  </button>
                </div>
                <div className="col-1 mt-3 ">
                  <Whisper
                    placement="auto"
                    trigger="click"
                    speaker={
                      <MenuPopover
                        selectedWeek={selectedWeek}
                        checkedDays={checkedDays}
                        setCheckedDays={setCheckedDays}
                        onSelect={handleApply}
                      />
                    }
                  >
                    <Button onClick={() => handleCopyClick(day)}>
                      <CopyIcon style={{ fontSize: 20, cursor: "pointer" }} />
                    </Button>
                  </Whisper>
                </div>
              </div>
            ))}
          </div>
        </div>
      </Accordion.Panel>
    </Accordion>
  );
};

export default WeeklyHours;












/* eslint-disable react/prop-types */
/* eslint-disable react/display-name */

import { useEffect, useState } from "react";
import "rsuite/dist/rsuite.min.css";
import PlusRoundIcon from "@rsuite/icons/PlusRound";
import MinusRoundIcon from "@rsuite/icons/MinusRound";
import CopyIcon from "@rsuite/icons/Copy";
import { DatePicker, Checkbox } from "rsuite";
import { forwardRef } from "react";
import { Popover, Whisper, Button, Dropdown } from "rsuite";
import { Accordion } from "rsuite";

const daysOfWeek = [
  "Sunday",
  "Monday",
  "Tuesday",
  "Wednesday",
  "Thursday",
  "Friday",
  "Saturday",
];
const MenuPopover = forwardRef(
  (
    {
      selectedWeek,
      onSelect,
      checkedDays,
      setCheckedDays,
      handleClose,
      ...rest
    },
    ref
  ) => (
    <Popover ref={ref} {...rest} full>
      <Dropdown.Menu>
        {daysOfWeek.map((day, index) => (
          <Dropdown.Item
            key={`${day}-${index}`} // Ensure unique key
            eventKey={day}
            onSelect={() => {
              // Toggle checkedDays state properly
              setCheckedDays((prev) => ({
                ...prev,
                [day]: !prev[day],
              }));
            }}
          >
            <Checkbox
              checked={checkedDays[day] || day === selectedWeek}
              disabled={day === selectedWeek}
            >
              {day}
            </Checkbox>
          </Dropdown.Item>
        ))}
        <Dropdown.Item eventKey="apply">
          <button
            className="btn btn-primary"
            onClick={() => {
              const selectedDays = Object.keys(checkedDays).filter(
                (d) => checkedDays[d]
              );
              if (selectedDays.length > 0) {
                onSelect(selectedDays);
              }
              handleClose(); // Close popover after applying
            }}
          >
            Apply
          </button>
        </Dropdown.Item>
      </Dropdown.Menu>
    </Popover>
  )
);

// const MenuPopover = forwardRef(
//   ({ selectedWeek, onSelect, checkedDays, setCheckedDays,  handleClose ,...rest }, ref) => (
//     <Popover ref={ref} {...rest} full>
//       <Dropdown.Menu>
//         {daysOfWeek.map((day) => (
//           <Dropdown.Item
//             key={day}
//             eventKey={day}
//             onSelect={() =>
//               setCheckedDays((prev) => ({ ...prev, [day]: !prev[day] }))
//             }
//           >
//             <Checkbox
//               checked={checkedDays[day] || day === selectedWeek}
//               disabled={day === selectedWeek}
//             >
//               {day}
//             </Checkbox>
//           </Dropdown.Item>
//         ))}
//         <Dropdown.Item eventKey="apply">
//         <button className="btn btn-primary" onClick={() => { onSelect(Object.keys(checkedDays).filter((day) => checkedDays[day]));
//            handleClose();
//          }}>
//         Apply
//           </button>
//         </Dropdown.Item>
//       </Dropdown.Menu>
//     </Popover>
//   )
// );
const WeeklyHours = ({
  register,
  WeekAppend,
  watch,
  WeekRemove,
  WeekFields,
  errors,
  setValue,
  setError,
  clearErrors,
  trigger,
  getValues,
}) => {
  const [openPopovers, setOpenPopovers] = useState({}); // Track open state per day

  const [selectedWeek, setSelectedWeek] = useState(null);
  const [checkedDays, setCheckedDays] = useState({});
  // daysOfWeek.reduce((acc, day) => ({ ...acc, [day]: day === selectedWeek }), {})

  useEffect(() => {
    WeekFields.forEach((_, index) => {
      daysOfWeek.forEach((day) => {
        register(`week[${index}].${day}.startDate`);
        register(`week[${index}].${day}.endDate`);
        register(`week[${index}].${day}.checked`);
      });
    });
  }, [WeekFields, register]);

  // const handleCopyClick = (day) => {
  //   setOpen(true);
  //   setSelectedWeek(day);

  //   // Ensure checkedDays only initializes once properly
  //   setCheckedDays(() => {
  //     const initialCheckedDays = daysOfWeek.reduce((acc, d) => {
  //       acc[d] = d === day; // Only mark selected day initially
  //       return acc;
  //     }, {});

  //     return initialCheckedDays;
  //   });
  // };

  const handleCopyClick = (day) => {
    setSelectedWeek(day);

    // Initialize checkedDays properly
    setCheckedDays(() =>
      daysOfWeek.reduce((acc, d) => {
        acc[d] = d === day;
        return acc;
      }, {})
    );

    // Close all popovers and open only for the clicked day
    setOpenPopovers((prev) => ({
      ...Object.keys(prev).reduce((acc, key) => {
        acc[key] = false; // Close all other popovers
        return acc;
      }, {}),
      [day]: true, // Open only for the clicked day
    }));
  };

  const handleApply = async (days) => {
    if (!days.length) return;
    const sourceIndexes = WeekFields.map((entry, index) =>
      entry[selectedWeek]?.checked ? index : -1
    ).filter((index) => index !== -1);

    if (sourceIndexes.length === 0) {
      return;
    }
    const currentValues = getValues();
    const copiedEntries = sourceIndexes.map((index) => ({
      startDate: currentValues.WeekFields[index][selectedWeek]?.startDate,
      endDate: currentValues.WeekFields[index][selectedWeek]?.endDate,
    }));

    if (copiedEntries.length === 0) {
      console.error("No valid entries found in source indexes.");
      return;
    }
    let newEntries = [];
    let updatedIndexes = {};
    for (const day of days) {
      let targetIndexes = WeekFields.map((entry, index) =>
        entry[day]?.checked ? index : -1
      ).filter((index) => index !== -1);

      if (targetIndexes.length === 0) {
        copiedEntries.forEach((entry) => {
          newEntries.push({
            [day]: {
              checked: true,
              startDate: entry.startDate,
              endDate: entry.endDate,
            },
          });
        });
      } else {
        targetIndexes.forEach((targetIndex) => {
          updatedIndexes[day] = updatedIndexes[day] || [];
          updatedIndexes[day].push(targetIndex);
        });
      }
    }
    if (newEntries.length > 0) {
      WeekAppend(newEntries);
      const startIndex = WeekFields.length;
      newEntries.forEach((entry, index) => {
        const day = Object.keys(entry)[0];
        updatedIndexes[day] = updatedIndexes[day] || [];
        updatedIndexes[day].push(startIndex + index);
      });
    }
    for (const day of days) {
      if (updatedIndexes[day]) {
        updatedIndexes[day].forEach((targetIndex, i) => {
          setValue(
            `WeekFields[${targetIndex}].${day}.startDate`,
            copiedEntries[i % copiedEntries.length].startDate
          );
          trigger(`WeekFields[${targetIndex}].${day}.startDate`);

          setValue(
            `WeekFields[${targetIndex}].${day}.endDate`,
            copiedEntries[i % copiedEntries.length].endDate,
            {
              shouldDirty: true,
              shouldTouch: true,
              shouldValidate: true,
            }
          );

          trigger(`WeekFields[${targetIndex}].${day}.endDate`);
        });
      }
    }
    await trigger();
    clearErrors();
  };
  const handleCheckboxChange = (day) => {
    const isChecked = WeekFields.some((entry) => entry[day]?.checked);
    if (!isChecked) {
      WeekAppend({
        [day]: { checked: true, startDate: null, endDate: null },
      });
      const newIndex = WeekFields.length;
      register(`WeekFields[${newIndex}].${day}.startDate`);
      register(`WeekFields[${newIndex}].${day}.endDate`);
      register(`WeekFields[${newIndex}].${day}.checked`);
    } else {
      const index = WeekFields.findIndex((entry) => entry[day]?.checked);
      if (index !== -1) {
        WeekRemove(index);
      }
    }
  };
  // const handleAppend = (day) => {
  //   const currentValues = getValues("WeekFields");
  //   let allFieldsFilled = true;

  //   currentValues.forEach((item, index) => {
  //     if (!item[day]?.startDate) {
  //       setError(`WeekFields[${index}].${day}.startDate`, {
  //         type: "manual",
  //         message: "Start time is required",
  //       });
  //       allFieldsFilled = false;
  //     }
  //     if (!item[day]?.endDate) {
  //       setError(`WeekFields[${index}].${day}.endDate`, {
  //         type: "manual",
  //         message: "End time is required",
  //       });
  //       allFieldsFilled = false;
  //     }
  //   });

  //   if (!allFieldsFilled) {
  //     WeekAppend(
  //        { checked: true, startDate: "", endDate: "" },
  //     );

  //       const updatedValues = getValues("WeekFields");
  //       const newIndex = updatedValues.length - 1;

  //       register(`WeekFields[${newIndex}].${day}.startDate`);
  //       register(`WeekFields[${newIndex}].${day}.endDate`);
  //       register(`WeekFields[${newIndex}].${day}.checked`);

  //       console.log(`New field appended for ${day} at index ${newIndex}`);

  //   } else {
  //     console.log("Cannot append, fill all fields first.");
  //   }
  // };

  const handleAppend = (day) => {
    const currentValues = getValues("WeekFields") || [];
    let allFieldsFilled = true;

    currentValues.forEach((item, index) => {
      if (!item[day]?.startDate) {
        setError(`WeekFields[${index}].${day}.startDate`, {
          type: "manual",
          message: "Start time is required",
        });
        allFieldsFilled = false;
      }
      if (!item[day]?.endDate) {
        setError(`WeekFields[${index}].${day}.endDate`, {
          type: "manual",
          message: "End time is required",
        });
        allFieldsFilled = false;
      }
    });

    if (allFieldsFilled) {
      WeekAppend({
        [day]: {
          checked: true,
          startDate: "",
          endDate: "",
        },
      });

      console.log(`New field appended for ${day}`);
    } else {
      console.log("Cannot append, fill all fields first.");
    }
  };

  return (
    <Accordion>
      <Accordion.Panel header="Weekly Hours " defaultExpanded>
        <div className="container mt-3 card">
          <div className="card-body">
            {daysOfWeek.map((day) => (
              <div className="p-1 row" key={day}>
                <div className="d-flex align-items-center col-2 ">
                  <Checkbox
                    checked={WeekFields.some((entry) => entry[day]?.checked)}
                    onChange={() => handleCheckboxChange(day)}
                  >
                    {day}
                  </Checkbox>
                </div>
                <div className="col-6">
                  {WeekFields.some((entry) => entry[day]?.checked) ? (
                    WeekFields.map((item, index) =>
                      item[day]?.checked ? (
                        <div key={index} className="row mt-2">
                          <div className="col-md-4">
                            <label>Start time</label>
                            <DatePicker
                              format="HH:mm"
                              editable={false}
                              value={watch(
                                `WeekFields[${index}].${day}.startDate`
                              )}
                              onChange={(date) => {
                                setValue(
                                  `WeekFields[${index}].${day}.startDate`,
                                  date
                                );
                                trigger(
                                  `WeekFields[${index}].${day}.startDate`
                                );
                              }}
                            />
                            {errors.WeekFields?.[index]?.[day]?.startDate && (
                              <p className="text-danger">
                                {
                                  errors.WeekFields[index][day].startDate
                                    .message
                                }
                              </p>
                            )}
                          </div>
                          <div className="col-md-4">
                            <label>End time</label>
                            <DatePicker
                              format="HH:mm"
                              editable={false}
                              value={watch(
                                `WeekFields[${index}].${day}.endDate`
                              )}
                              onChange={(date) => {
                                setValue(
                                  `WeekFields[${index}].${day}.endDate`,
                                  date
                                );
                                trigger(`WeekFields[${index}].${day}.endDate`);
                              }}
                            />
                            {errors.WeekFields?.[index]?.[day]?.endDate && (
                              <p className="text-danger">
                                {errors.WeekFields[index][day].endDate.message}
                              </p>
                            )}
                          </div>
                          <div className="mt-3 col-2">
                            <button
                              type="button"
                              onClick={() => WeekRemove(index)}
                            >
                              <MinusRoundIcon style={{ fontSize: 15 }} />
                            </button>
                          </div>
                        </div>
                      ) : null
                    )
                  ) : (
                    <p className="pt-3">Unavailable</p>
                  )}
                </div>
                <div className="col-1 mt-3 mx-5">
                  <button type="button" onClick={() => handleAppend(day)}>
                    <PlusRoundIcon style={{ fontSize: 20 }} />
                  </button>
                </div>
                <div className="col-1 mt-3 ">
                  {/* <Whisper
                      placement="auto"
                      trigger="click"
                      speaker={
                        <MenuPopover
                          selectedWeek={selectedWeek}
                          checkedDays={checkedDays}
                          setCheckedDays={setCheckedDays}
                          onSelect={handleApply}
                        />
                      }
                    >
                      <Button onClick={() => handleCopyClick(day)}>
                        <CopyIcon style={{ fontSize: 20, cursor: "pointer" }} />
                      </Button>
                    </Whisper> */}
                  {/* <Whisper
                    placement="auto"
                    trigger="click"
                    open={open} // Control open state
                    onClose={() => setOpen(false)} // Close popover when clicking outside
                    speaker={
                      <MenuPopover
                        selectedWeek={selectedWeek}
                        checkedDays={checkedDays}
                        setCheckedDays={setCheckedDays}
                        onSelect={handleApply}
                        handleClose={() => setOpen(false)} // Close popover on Apply click
                      />
                    }
                  >
                    <Button 
                      onAbortnClick={() => handleCopyClick(day)}
                      >
                     
                    
                      <CopyIcon style={{ fontSize: 20, cursor: "pointer" }} />
                    </Button>
                  </Whisper> */}

                  <Whisper
                    placement="auto"
                    trigger="click"
                    open={openPopovers[day] || false} // Open only for the clicked day
                    onClose={() =>
                      setOpenPopovers((prev) => ({ ...prev, [day]: false }))
                    } // Close popover when clicking outside
                    speaker={
                      <MenuPopover
                        selectedWeek={selectedWeek}
                        checkedDays={checkedDays}
                        setCheckedDays={setCheckedDays}
                        onSelect={handleApply}
                        handleClose={() =>
                          setOpenPopovers((prev) => ({ ...prev, [day]: false }))
                        } // Close popover on Apply click
                      />
                    }
                  >
                    <Button onClick={() => handleCopyClick(day)}>
                      <CopyIcon style={{ fontSize: 20, cursor: "pointer" }} />
                    </Button>
                  </Whisper>
                </div>
              </div>
            ))}
          </div>
        </div>
      </Accordion.Panel>
    </Accordion>
  );
};

export default WeeklyHours;





// const express = require("express");
// const { MongoClient, ObjectId } = require("mongodb");
// const cors = require("cors");
// const app = express();
// const port = 4002;
// const { DateTime } = require("luxon");
// const uri = "mongodb://localhost:2707";
// const client = new MongoClient(uri);
// const dbName = "createSlots";
// app.use(cors());
// app.use(express.json());
// function datas() {
//   return {
//     mainSchema: {
//       interviewID: "",
//       campaignID: "",
//       roundNumber: 1,
//       startDate: "",
//       endDate: "",
//       selected: false,
//       deleted: false,
//       event: "",
//       allowJobseekerToReschedule: true,
//       userID: "",
//       resumeID: "",
//       scheduledType: "",
//       sourceOfBooking: [],
//       availableMeetTypes: [],
//       selectedMeetType: "",
//       sourceOfDeletion: "",
//       duration: 30,
//       timeZone: "",
//       timeZoneName: "",
//       timeZoneFullName: "",
//       sourceOfCreation: "Auto Fill",
//       description: "",
//       participants: [],
//       location: {},
//       phones: [],
//       createdAt: "",
//       createdBy: "",
//       deletedAt: "",
//       autoDelete: true,
//       deletedBy: "",
//       companyID: "",
//       clientID: "",
//     },
//     listSchema: {
//       phones: {
//         phoneNumber: "",
//         internationalPhoneCode: "",
//       },
//       participants: {
//         userID: "",
//         email: "",
//         name: "",
//         host: false,
//         confirmed: "",
//         notes: "",
//         comment: "",
//         rating: 0,
//         liveURL: "",
//       },
//     },
//     values: {
//       availableMeetTypes: ["In-Person", "Live Video"],
//       scheduledType: ["Auto Schedule", "Direct Schedule"],
//       sourceOfCreation: ["Auto Fill", "Manual"],
//       sourceOfDeletion: ["Sync", "User"],
//       sourceOfBooking: ["Recruiter", "Chatbot", "Slot Booking UI"],
//     },
//   };
// }

// app.post("/api/slots/", async (req, res) => {
//   try {
//     await client.connect();
//     const db = client.db(dbName);
//     const data = req.body;
//     // console.log("Data:", data.data);
//     let slotschema = await datas();
//     const slotsSCHEMA = slotschema.mainSchema;

//     if (data.data.startDate) {
//       slotsSCHEMA.startDate = DateTime.fromISO(data.data.startDate, { zone: "utc" }).toUTC().toISO();

//     }
//     if (data.data.endDate) {
//       slotsSCHEMA.endDate = DateTime.fromISO(data.data.endDate, { zone: "utc" }).toFormat("yyyy-MM-dd'T'HH:mm:ss'Z'");

//     }
//     if (data.data.duration) {
//       slotsSCHEMA.duration = data.data.duration;
//     }

//     if (data.data.Description) {
//       slotsSCHEMA.description = data.data.Description;
//     }
   let WeeklyHours = [];
   for (let i of data.data.WeekFields) {
     let dayName = Object.keys(i)[0];
     let { startDate, endDate } = i[dayName];
     let startIST = DateTime.fromISO(startDate, { zone: "utc" })
       .setZone("Asia/Kolkata")
       .toFormat(" HH:mm:ss");
     let endIST = DateTime.fromISO(endDate, { zone: "utc" })
       .setZone("Asia/Kolkata")
       .toFormat(" HH:mm:ss");
     WeeklyHours.push(`${dayName}: Start - ${startIST}, End - ${endIST}`);
  }
/   let BreakTime = [];

//   //  for(let j of data.data.time){
//   //   console.log(j)
    
//   //  }
    
//   //   console.log("BreakTime:", BreakTime);
    



//     const result = await db
//       .collection("praveenresumeDBSchema")
//       .insertOne(slotsSCHEMA);
//     res.status(201).json({ message: "Slot created successfully", result });
//   } catch (error) {
//     console.error("Error creating slot:", error);
//     res.status(500).json({ message: "Error creating slot", error });
//   }
// });
// app.listen(port, () => {
//   console.log(`Server running at http://localhost:${port}`);
// });






it working  ...













const express = require("express");
const { MongoClient } = require("mongodb");
const cors = require("cors");
const { DateTime } = require("luxon");

const app = express();
const port = 4003;
const uri = "mongodb://localhost:27017";
const client = new MongoClient(uri);
const dbName = "createSlots";

app.use(cors());
app.use(express.json());
function datas() {
  return {
    mainSchema: {
      interviewID: "",
      campaignID: "",
      roundNumber: 1,
      startDate: "",
      endDate: "",
      selected: false,
      deleted: false,
      event: "",
      allowJobseekerToReschedule: true,
      userID: "",
      resumeID: "",
      scheduledType: "",
      sourceOfBooking: [],
      availableMeetTypes: [],
      selectedMeetType: "",
      sourceOfDeletion: "",
      duration: 30,
      timeZone: "",
      timeZoneName: "",
      timeZoneFullName: "",
      sourceOfCreation: "Auto Fill",
      description: "",
      participants: [],
      location: {},
      phones: [],
      createdAt: "",
      createdBy: "",
      deletedAt: "",
      autoDelete: true,
      deletedBy: "",
      companyID: "",
      clientID: "",
    },
    listSchema: {
      phones: {
        phoneNumber: "",
        internationalPhoneCode: "",
      },
      participants: {
        userID: "",
        email: "",
        name: "",
        host: false,
        confirmed: "",
        notes: "",
        comment: "",
        rating: 0,
        liveURL: "",
      },
    },
    values: {
      availableMeetTypes: ["In-Person", "Live Video"],
      scheduledType: ["Auto Schedule", "Direct Schedule"],
      sourceOfCreation: ["Auto Fill", "Manual"],
      sourceOfDeletion: ["Sync", "User"],
      sourceOfBooking: ["Recruiter", "Chatbot", "Slot Booking UI"],
    },
  };
}

app.post("/api/slots/", async (req, res) => {
  try {
    await client.connect();
    const db = client.db(dbName);
    const data = req.body.data;
    if (
      !data.startDate ||
      !data.endDate ||
      !data.duration ||
      !data.WeekFields
    ) {
      return res.status(400).json({ message: "Missing required fields!" });
    }
    let startDate = DateTime.fromISO(data.startDate, { zone: "utc" }).toUTC();
    let endDate = DateTime.fromISO(data.endDate, { zone: "utc" }).toUTC();
    let duration = parseInt(data.duration.replace("min", ""), 10);

    let slots = [];
    let currentDate = startDate;

    while (currentDate <= endDate) {
      let weekdayName = currentDate.toFormat("EEEE"); // Monday, Tuesday, etc.

      // 🔹 Find working hours for this weekday
      let daySchedule = data.WeekFields.find((item) => item[weekdayName]);

      if (!daySchedule || !daySchedule[weekdayName]) {
        console.warn(`⚠️ No working hours for ${weekdayName}, skipping.`);
        currentDate = currentDate.plus({ days: 1 });
        continue;
      }

      let { startDate: startTime, endDate: endTime } =
        daySchedule[weekdayName] || {};

      if (!startTime || !endTime) {
        console.warn(
          `⚠️ Invalid time for ${weekdayName}: Start - ${startTime}, End - ${endTime}`
        );
        currentDate = currentDate.plus({ days: 1 });
        continue;
      }

      // 🔹 Convert to correct timezone and adjust to the currentDate
      let workStart = DateTime.fromISO(startTime, { zone: "utc" })
        .setZone("Asia/Kolkata")
        .set({
          year: currentDate.year,
          month: currentDate.month,
          day: currentDate.day,
        });

      let workEnd = DateTime.fromISO(endTime, { zone: "utc" })
        .setZone("Asia/Kolkata")
        .set({
          year: currentDate.year,
          month: currentDate.month,
          day: currentDate.day,
        });

      let slotStart = workStart;
      while (slotStart.plus({ minutes: duration }) <= workEnd) {
        let slotSchema = ({...datas().mainSchema})
        slotSchema.startDate = slotStart.toISO();
        console.log(slotSchema)
        slotSchema.endDate = slotStart.plus({ minutes: duration }).toISO();
        slotSchema.duration = duration;
        slotSchema.description = data.description || "";
        slotSchema.timeZone = "Asia/Kolkata";

        slots.push(slotSchema);
        slotStart = slotStart.plus({ minutes: duration });
      }

      currentDate = currentDate.plus({ days: 1 });
    }

    if (slots.length > 0) {
      const result = await db.collection("SlotsDBSchema").insertMany(slots);
      res.status(201).json({
        message: "Slots created successfully",
        slots: result.insertedIds,
      });
    } else {
      res
        .status(200)
        .json({ message: "No slots generated due to constraints." });
    }
  } catch (error) {
    console.error("Error creating slots:", error);
    res.status(500).json({ message: "Error creating slots", error });
  }
});

app.listen(port, () => {
  console.log(`🚀 Server running at http://localhost:${port}`);
});



/////////////////////////////////



const express = require("express");
const { MongoClient } = require("mongodb");
const cors = require("cors");
const { DateTime } = require("luxon");

const app = express();
const port = 5000;
const uri = "mongodb://localhost:27017";
const client = new MongoClient(uri);
const dbName = "createSlots";

app.use(cors());
app.use(express.json());
function datas() {
  return {
    mainSchema: {
      interviewID: "",
      campaignID: "",
      roundNumber: 1,
      startDate: "",
      endDate: "",
      selected: false,
      deleted: false,
      event: "",
      allowJobseekerToReschedule: true,
      userID: "",
      resumeID: "",
      scheduledType: "",
      sourceOfBooking: [],
      availableMeetTypes: [],
      selectedMeetType: "",
      sourceOfDeletion: "",
      duration: 30,
      timeZone: "",
      timeZoneName: "",
      timeZoneFullName: "",
      sourceOfCreation: "Auto Fill",
      description: "",
      participants: [],
      location: {},
      phones: [],
      createdAt: "",
      createdBy: "",
      deletedAt: "",
      autoDelete: true,
      deletedBy: "",
      companyID: "",
      clientID: "",
    },
    listSchema: {
      phones: {
        phoneNumber: "",
        internationalPhoneCode: "",
      },
      participants: {
        userID: "",
        email: "",
        name: "",
        host: false,
        confirmed: "",
        notes: "",
        comment: "",
        rating: 0,
        liveURL: "",
      },
    },
    values: {
      availableMeetTypes: ["In-Person", "Live Video"],
      scheduledType: ["Auto Schedule", "Direct Schedule"],
      sourceOfCreation: ["Auto Fill", "Manual"],
      sourceOfDeletion: ["Sync", "User"],
      sourceOfBooking: ["Recruiter", "Chatbot", "Slot Booking UI"],
    },
  };
}

// app.post("/api/slots/", async (req, res) => {
//   try {
//     await client.connect();
//     const db = client.db(dbName);
//     const data = req.body.data;

//     let startDate = DateTime.fromISO(data.startDate, { zone: "utc" }).toUTC();
//     let endDate = DateTime.fromISO(data.endDate, { zone: "utc" }).toUTC();
//     let duration = parseInt(data.duration.replace("min", ""), 10);

//     let slots = [];
//     let currentDate = startDate;

//     while (currentDate <= endDate) {
//       let weekdayName = currentDate.toFormat("EEEE"); // Monday, Tuesday, etc.
//       let workStart, workEnd;

//       // 🔹 Check if WeekFields exist and contains a schedule for this day
//       if (data.WeekFields && data.WeekFields.length > 0) {
//         let daySchedule = data.WeekFields.find((item) => item[weekdayName]);

//         if (daySchedule && daySchedule[weekdayName]) {
//           let { startDate: startTime, endDate: endTime } = daySchedule[weekdayName];

//           if (startTime && endTime) {
//             workStart = DateTime.fromISO(startTime, { zone: "utc" })
//               .setZone("Asia/Kolkata")
//               .set({ year: currentDate.year, month: currentDate.month, day: currentDate.day });

//             workEnd = DateTime.fromISO(endTime, { zone: "utc" })
//               .setZone("Asia/Kolkata")
//               .set({ year: currentDate.year, month: currentDate.month, day: currentDate.day });
//           }
//         }
//       }

//       // 🔹 If WeekFields is missing or this weekday is not found, default to startDate
//       if (!workStart || !workEnd) {
//         console.warn(`⚠️ No working hours for ${weekdayName}. Using provided startDate.`);
//         workStart = startDate.setZone("Asia/Kolkata");
//         workEnd = endDate.setZone("Asia/Kolkata");
//       }

//       // 🔹 Generate time slots
//       let slotStart = workStart;
//       while (slotStart.plus({ minutes: duration }) <= workEnd) {
//         let slotSchema = { ...datas().mainSchema };
//         slotSchema.startDate = slotStart.toISO();
//         slotSchema.endDate = slotStart.plus({ minutes: duration }).toISO();
//         slotSchema.duration = duration;
//         slotSchema.description = data.description || "";
//         slotSchema.timeZone = "Asia/Kolkata";

//         slots.push(slotSchema);
//         slotStart = slotStart.plus({ minutes: duration });
//       }

//       currentDate = currentDate.plus({ days: 1 });
//     }

//     if (slots.length > 0) {
//       const result = await db.collection("SlotsDBSchema").insertMany(slots);
//       res.status(201).json({
//         message: "Slots created successfully",
//         slots: result.insertedIds,
//       });
//     } else {
//       res.status(200).json({ message: "No slots generated due to constraints." });
//     }
//   } catch (error) {
//     console.error("Error creating slots:", error);
//     res.status(500).json({ message: "Error creating slots", error });
//   }
// });

app.post("/api/slots/", async (req, res) => {
  try {
    await client.connect();
    const db = client.db(dbName);
    const data = req.body.data;

    let startDate = DateTime.fromISO(data.startDate, { zone: "utc" }).toUTC().toJSDate();
    let endDate = DateTime.fromISO(data.endDate, { zone: "utc" }).toUTC().toJSDate();
    let duration = parseInt(data.duration.replace("min", ""), 10);
    let slots = [];
    let currentDate = DateTime.fromJSDate(startDate); //  Convert back to Luxon DateTime

    while (currentDate <= endDate) {
      let weekdayName = currentDate.toFormat("EEEE"); 
      let workStart, workEnd;

      //  Check if WeekFields exist and contains a schedule for this day
      if (data.WeekFields && data.WeekFields.length > 0) {
        let daySchedule = data.WeekFields.find((item) => item[weekdayName]);

        if (daySchedule && daySchedule[weekdayName]) {
          let { startDate: startTime, endDate: endTime } = daySchedule[weekdayName];

          if (startTime && endTime) {
            workStart = DateTime.fromISO(startTime, { zone: "utc" })
              .setZone("Asia/Kolkata")
              .set({ year: currentDate.year, month: currentDate.month, day: currentDate.day });

            workEnd = DateTime.fromISO(endTime, { zone: "utc" })
              .setZone("Asia/Kolkata")
              .set({ year: currentDate.year, month: currentDate.month, day: currentDate.day });
          }
        }
      }

      // 🔹 If WeekFields is missing or this weekday is not found, use the current time until 12 PM
      if (!workStart || !workEnd) {
        console.warn(`⚠️ No working hours for ${weekdayName}. Using current time to 12 PM.`);

        let now = DateTime.now().setZone("Asia/Kolkata");
        workStart = now.startOf("hour"); // Round to the nearest hour
        workEnd = now.set({ hour: 12, minute: 0, second: 0, millisecond: 0 });

        // Ensure that workEnd is not before workStart
        if (workEnd <= workStart) {
          workEnd = workStart.plus({ hours: 2 }); // Default to a 2-hour window if it's already past 12 PM
        }
      }

      // 🔹 Generate time slots
      let slotStart = workStart;
      while (slotStart.plus({ minutes: duration }) <= workEnd) {
        let slotSchema = { ...datas().mainSchema };
        slotSchema.startDate = slotStart.toJSDate();
        slotSchema.endDate = slotStart.plus({ minutes: duration }).toJSDate();
        slotSchema.duration = duration;
        slotSchema.description = data.description || "";
        slotSchema.timeZone = "Asia/Kolkata";

        slots.push(slotSchema);
        slotStart = slotStart.plus({ minutes: duration });
      }

      currentDate = currentDate.plus({ days: 1 });
    }

    if (slots.length > 0) {
      const result = await db.collection("SlotsDBSchema").insertMany(slots);
      res.status(201).json({
        message: "Slots created successfully",
        slots: result.insertedIds,
      });
    } else {
      res.status(200).json({ message: "No slots generated due to constraints." });
    }
  } catch (error) {
    console.error("Error creating slots:", error);
    res.status(500).json({ message: "Error creating slots", error });
  }
});

app.listen(port, () => {
  console.log(`🚀 Server running at http://localhost:${port}`);
});















//////////break hours 









// const express = require("express");
// const { MongoClient } = require("mongodb");
// const cors = require("cors");
// const { DateTime } = require("luxon");

// const app = express();
// const port = 5001;
// const uri = "mongodb://localhost:27017";
// const client = new MongoClient(uri);
// const dbName = "createSlots";

// app.use(cors());
// app.use(express.json());

// function datas() {
//   return {
//     mainSchema: {
//       interviewID: "",
//       campaignID: "",
//       roundNumber: 1,
//       startDate: "",
//       endDate: "",
//       selected: false,
//       deleted: false,
//       event: "",
//       allowJobseekerToReschedule: true,
//       userID: "",
//       resumeID: "",
//       scheduledType: "",
//       sourceOfBooking: [],
//       availableMeetTypes: [],
//       selectedMeetType: "",
//       sourceOfDeletion: "",
//       duration: 30,
//       timeZone: "",
//       timeZoneName: "",
//       timeZoneFullName: "",
//       sourceOfCreation: "Auto Fill",
//       description: "",
//       participants: [],
//       location: {},
//       phones: [],
//       createdAt: "",
//       createdBy: "",
//       deletedAt: "",
//       autoDelete: true,
//       deletedBy: "",
//       companyID: "",
//       clientID: "",
//     },
//   };
// }

// app.post("/api/slots/", async (req, res) => {
//   try {
//     await client.connect();
//     const db = client.db(dbName);
//     const data = req.body.data;

//     // Convert break periods to Luxon DateTime in 'Asia/Kolkata' timezone
//     let breakPeriods = (data.time || []).map((breakHour) => ({
//       start: DateTime.fromISO(breakHour.startime, { zone: "utc" }).setZone("Asia/Kolkata"),
//       end: DateTime.fromISO(breakHour.endtime, { zone: "utc" }).setZone("Asia/Kolkata"),
//     }));

//     console.log(breakPeriods, "Break Periods"); // Debugging

//     let startDate = DateTime.fromISO(data.startDate, { zone: "utc" }).setZone("Asia/Kolkata");
//     let endDate = DateTime.fromISO(data.endDate, { zone: "utc" }).setZone("Asia/Kolkata");
//     let duration = parseInt(data.duration.replace("min", ""), 10);
//     let slots = [];
//     let currentDate = startDate;

//     while (currentDate <= endDate) {
//       let weekdayName = currentDate.toFormat("EEEE");
//       let workStart, workEnd;

//       // Fetch working hours from WeekFields
//       if (data.WeekFields && data.WeekFields.length > 0) {
//         let daySchedule = data.WeekFields.find((item) => item[weekdayName]);

//         if (daySchedule && daySchedule[weekdayName]) {
//           let { startDate: startTime, endDate: endTime } = daySchedule[weekdayName];

//           if (startTime && endTime) {
//             workStart = DateTime.fromISO(startTime, { zone: "utc" })
//               .setZone("Asia/Kolkata")
//               .set({ year: currentDate.year, month: currentDate.month, day: currentDate.day });

//             workEnd = DateTime.fromISO(endTime, { zone: "utc" })
//               .setZone("Asia/Kolkata")
//               .set({ year: currentDate.year, month: currentDate.month, day: currentDate.day });
//           }
//         }
//       }

//       // Default working hours if missing
//       if (!workStart || !workEnd) {
//         console.warn(`⚠️ No working hours for ${weekdayName}. Defaulting to 9 AM - 6 PM.`);
//         workStart = currentDate.set({ hour: 9, minute: 0 });
//         workEnd = currentDate.set({ hour: 18, minute: 0 });
//       }

//       let slotStart = workStart;
//       while (slotStart.plus({ minutes: duration }) <= workEnd) {
//         let slotEnd = slotStart.plus({ minutes: duration });

//         // Ensure `slotStart` and `slotEnd` are in 'Asia/Kolkata'
//         slotStart = slotStart.setZone("Asia/Kolkata");
//         slotEnd = slotEnd.setZone("Asia/Kolkata");

//         // Debugging - Print slot times
//         console.log(`Checking slot: ${slotStart.toISO()} - ${slotEnd.toISO()}`);

//         // **🚀 Fix: Ensure slot does NOT overlap with break periods**
//         let isBreakTime = breakPeriods.some((breakPeriod) => {
//           let breakStart = breakPeriod.start;
//           let breakEnd = breakPeriod.end;

//           console.log(
//             `Break: ${breakStart.toISO()} - ${breakEnd.toISO()} | Slot: ${slotStart.toISO()} - ${slotEnd.toISO()}`
//           );

//           return (
//             (slotStart >= breakStart && slotStart < breakEnd) || // Slot starts in break
//             (slotEnd > breakStart && slotEnd <= breakEnd) || // Slot ends in break
//             (slotStart <= breakStart && slotEnd >= breakEnd) // Slot fully covers break
//           );
//         });

//         if (!isBreakTime) {
//           let slotSchema = { ...datas().mainSchema };
//           slotSchema.startDate = slotStart.toISO();
//           slotSchema.endDate = slotEnd.toISO();
//           slotSchema.duration = duration;
//           slotSchema.description = data.description || "";
//           slotSchema.timeZone = "Asia/Kolkata";

//           slots.push(slotSchema);
//         } else {
//           console.log(`❌ Removing slot: ${slotStart.toISO()} - ${slotEnd.toISO()} (Overlaps with break)`);
//         }

//         slotStart = slotEnd;
//       }

//       currentDate = currentDate.plus({ days: 1 });
//     }

//     console.log(slots, "Final Slots List"); // Debugging - check final slots

//     if (slots.length > 0) {
//       const result = await db.collection("SlotsDBSchema").insertMany(slots);
//       res.status(201).json({
//         message: "Slots created successfully (excluding break hours)",
//         slots: result.insertedIds,
//       });
//     } else {
//       res.status(200).json({ message: "No slots generated due to constraints." });
//     }
//   } catch (error) {
//     console.error("Error creating slots:", error);
//     res.status(500).json({ message: "Error creating slots", error });
//   }
// });

// app.listen(port, () => {
//   console.log(`🚀 Server running at http://localhost:${port}`);
// });











const express = require("express");
const { MongoClient } = require("mongodb");
const cors = require("cors");
const { DateTime } = require("luxon");

const app = express();
const port = 5001;
const uri = "mongodb://localhost:27017";
const client = new MongoClient(uri);
const dbName = "createSlots";

app.use(cors());
app.use(express.json());

function datas() {
  return {
    mainSchema: {
      interviewID: "",
      campaignID: "",
      roundNumber: 1,
      startDate: "",
      endDate: "",
      selected: false,
      deleted: false,
      event: "",
      allowJobseekerToReschedule: true,
      userID: "",
      resumeID: "",
      scheduledType: "",
      sourceOfBooking: [],
      availableMeetTypes: [],
      selectedMeetType: "",
      sourceOfDeletion: "",
      duration: 30,
      timeZone: "",
      timeZoneName: "",
      timeZoneFullName: "",
      sourceOfCreation: "Auto Fill",
      description: "",
      participants: [],
      location: {},
      phones: [],
      createdAt: "",
      createdBy: "",
      deletedAt: "",
      autoDelete: true,
      deletedBy: "",
      companyID: "",
      clientID: "",
    },
  };
}

app.post("/api/slots/", async (req, res) => {
  try {
    await client.connect();
    const db = client.db(dbName);
    const data = req.body.data;

    // Convert break periods to only use time (HH:mm) format
    let breakPeriods = (data.time || []).map((breakHour) => ({
      start: DateTime.fromISO(breakHour.startime, { zone: "utc" })
        .setZone("Asia/Kolkata")
        .toFormat("HH:mm"),
      end: DateTime.fromISO(breakHour.endtime, { zone: "utc" })
        .setZone("Asia/Kolkata")
        .toFormat("HH:mm"),
    }));

    console.log(breakPeriods, "Break Periods (Only Time)"); // Debugging

    let startDate = DateTime.fromISO(data.startDate, { zone: "utc" }).setZone("Asia/Kolkata");
    let endDate = DateTime.fromISO(data.endDate, { zone: "utc" }).setZone("Asia/Kolkata");
    let duration = parseInt(data.duration.replace("min", ""), 10);
    let slots = [];
    let currentDate = startDate;

    while (currentDate <= endDate) {
      let weekdayName = currentDate.toFormat("EEEE");
      let workStart, workEnd;

      // Fetch working hours from WeekFields
      if (data.WeekFields && data.WeekFields.length > 0) {
        let daySchedule = data.WeekFields.find((item) => item[weekdayName]);

        if (daySchedule && daySchedule[weekdayName]) {
          let { startDate: startTime, endDate: endTime } = daySchedule[weekdayName];

          if (startTime && endTime) {
            workStart = DateTime.fromISO(startTime, { zone: "utc" })
              .setZone("Asia/Kolkata")
              .set({ year: currentDate.year, month: currentDate.month, day: currentDate.day });

            workEnd = DateTime.fromISO(endTime, { zone: "utc" })
              .setZone("Asia/Kolkata")
              .set({ year: currentDate.year, month: currentDate.month, day: currentDate.day });
          }
        }
      }

      // Default working hours if missing
      if (!workStart || !workEnd) {
        console.warn(`⚠️ No working hours for ${weekdayName}. Defaulting to 9 AM - 6 PM.`);
        workStart = currentDate.set({ hour: 9, minute: 0 });
        workEnd = currentDate.set({ hour: 18, minute: 0 });
      }

      let slotStart = workStart;
      while (slotStart.plus({ minutes: duration }) <= workEnd) {
        let slotEnd = slotStart.plus({ minutes: duration });

        // Extract only time in HH:mm format
        let slotStartTime = slotStart.toFormat("HH:mm");
        let slotEndTime = slotEnd.toFormat("HH:mm");

        console.log(`Checking slot: ${slotStartTime} - ${slotEndTime}`);

        // Ensure slot does NOT overlap with break periods (only based on time)
        let isBreakTime = breakPeriods.some((breakPeriod) => {
          let breakStartTime = breakPeriod.start;
          let breakEndTime = breakPeriod.end;

          console.log(
            `Break: ${breakStartTime} - ${breakEndTime} | Slot: ${slotStartTime} - ${slotEndTime}`
          );

          return (
            (slotStartTime >= breakStartTime && slotStartTime < breakEndTime) || // Slot starts in break
            (slotEndTime > breakStartTime && slotEndTime <= breakEndTime) || // Slot ends in break
            (slotStartTime <= breakStartTime && slotEndTime >= breakEndTime) // Slot fully covers break
          );
        });

        if (!isBreakTime) {
          let slotSchema = { ...datas().mainSchema };
          slotSchema.startDate = slotStart.toISO();
          slotSchema.endDate = slotEnd.toISO();
          slotSchema.duration = duration;
          slotSchema.description = data.description || "";
          slotSchema.timeZone = "Asia/Kolkata";

          slots.push(slotSchema);
        } else {
          console.log(`❌ Removing slot: ${slotStartTime} - ${slotEndTime} (Overlaps with break)`);
        }

        slotStart = slotEnd;
      }

      currentDate = currentDate.plus({ days: 1 });
    }

    console.log(slots, "Final Slots List"); // Debugging - check final slots

    if (slots.length > 0) {
      const result = await db.collection("SlotsDBSchema").insertMany(slots);
      res.status(201).json({
        message: "Slots created successfully (excluding break hours)",
        slots: result.insertedIds,
      });
    } else {
      res.status(200).json({ message: "No slots generated due to constraints." });
    }
  } catch (error) {
    console.error("Error creating slots:", error);
    res.status(500).json({ message: "Error creating slots", error });
  }
});

app.listen(port, () => {
  console.log(`🚀 Server running at http://localhost:${port}`);
});



// holidays
//////////////////////////////////////////////////////////////////


const express = require("express");
const { MongoClient } = require("mongodb");
const cors = require("cors");
const { DateTime } = require("luxon");

const app = express();
const port = 5001;
const uri = "mongodb://localhost:27017";
const client = new MongoClient(uri);
const dbName = "createSlots";

app.use(cors());
app.use(express.json());

// Function to get default schema
function datas() {
  return {
    mainSchema: {
      interviewID: "",
      campaignID: "",
      roundNumber: 1,
      startDate: "",
      endDate: "",
      selected: false,
      deleted: false,
      event: "",
      allowJobseekerToReschedule: true,
      userID: "",
      resumeID: "",
      scheduledType: "",
      sourceOfBooking: [],
      availableMeetTypes: [],
      selectedMeetType: "",
      sourceOfDeletion: "",
      duration: 30,
      timeZone: "",
      timeZoneName: "",
      timeZoneFullName: "",
      sourceOfCreation: "Auto Fill",
      description: "",
      participants: [],
      location: {},
      phones: [],
      createdAt: "",
      createdBy: "",
      deletedAt: "",
      autoDelete: true,
      deletedBy: "",
      companyID: "",
      clientID: "",
    },
  };
}

app.post("/api/slots/", async (req, res) => {
  try {
    await client.connect();
    const db = client.db(dbName);
    const data = req.body.data;

    console.log(data.date, "Received holiday dates");

    let holidaySet = new Set();

    if (data.excludeHolidays) {
      data.date.forEach((holiday) => {
        let start = DateTime.fromISO(holiday.startDate).toISODate();
        let end = DateTime.fromISO(holiday.endDate).toISODate();

        let current = DateTime.fromISO(start);
        let endDate = DateTime.fromISO(end);

        while (current <= endDate) {
          holidaySet.add(current.toISODate());
          console.log(`🗓️ Adding Holiday: ${current.toISODate()}`);
          current = current.plus({ days: 1 });
        }
      });

      console.log(`🚫 Final Holiday Set:`, holidaySet);
    }

    // Convert break periods to HH:mm format
    let breakPeriods = (data.time || []).map((breakHour) => ({
      start: DateTime.fromISO(breakHour.startime, { zone: "utc" })
        .setZone("Asia/Kolkata")
        .toFormat("HH:mm"),
      end: DateTime.fromISO(breakHour.endtime, { zone: "utc" })
        .setZone("Asia/Kolkata")
        .toFormat("HH:mm"),
    }));

    console.log(breakPeriods, "Break Periods (Only Time)");

    let startDate = DateTime.fromISO(data.startDate, { zone: "utc" }).setZone("Asia/Kolkata");
    let endDate = DateTime.fromISO(data.endDate, { zone: "utc" }).setZone("Asia/Kolkata");
    let duration = parseInt(data.duration.replace("min", ""), 10);
    let slots = [];
    let currentDate = startDate;

    while (currentDate <= endDate) {
      let formattedDate = currentDate.toFormat("yyyy-MM-dd");

      // 🚫 Skip holidays
      if (holidaySet.has(formattedDate)) {
        console.log(`⛔ Skipping ${formattedDate}, it's a holiday.`);
        currentDate = currentDate.plus({ days: 1 });
        continue;
      }

      let weekdayName = currentDate.toFormat("EEEE");
      let workStart, workEnd;

      // Fetch working hours from WeekFields
      if (data.WeekFields && data.WeekFields.length > 0) {
        let daySchedule = data.WeekFields.find((item) => item[weekdayName]);

        if (daySchedule && daySchedule[weekdayName]) {
          let { startDate: startTime, endDate: endTime } = daySchedule[weekdayName];

          if (startTime && endTime) {
            workStart = DateTime.fromISO(startTime, { zone: "utc" })
              .setZone("Asia/Kolkata")
              .set({ year: currentDate.year, month: currentDate.month, day: currentDate.day });

            workEnd = DateTime.fromISO(endTime, { zone: "utc" })
              .setZone("Asia/Kolkata")
              .set({ year: currentDate.year, month: currentDate.month, day: currentDate.day });
          }
        }
      }

      // Default working hours if missing
      if (!workStart || !workEnd) {
        console.warn(`⚠️ No working hours for ${weekdayName}. Defaulting to 9 AM - 6 PM.`);
        workStart = currentDate.set({ hour: 9, minute: 0 });
        workEnd = currentDate.set({ hour: 18, minute: 0 });
      }

      let slotStart = workStart;
      while (slotStart.plus({ minutes: duration }) <= workEnd) {
        let slotEnd = slotStart.plus({ minutes: duration });

        let slotStartTime = slotStart.toFormat("HH:mm");
        let slotEndTime = slotEnd.toFormat("HH:mm");

        // Ensure slot does NOT overlap with break periods (only based on time)
        let isBreakTime = breakPeriods.some((breakPeriod) => {
          let breakStartTime = breakPeriod.start;
          let breakEndTime = breakPeriod.end;

          return (
            (slotStartTime >= breakStartTime && slotStartTime < breakEndTime) ||
            (slotEndTime > breakStartTime && slotEndTime <= breakEndTime) ||
            (slotStartTime <= breakStartTime && slotEndTime >= breakEndTime)
          );
        });

        if (!isBreakTime) {
          let slotSchema = { ...datas().mainSchema };
          slotSchema.startDate = slotStart.toISO();
          slotSchema.endDate = slotEnd.toISO();
          slotSchema.duration = duration;
          slotSchema.description = data.description || "";
          slotSchema.timeZone = "Asia/Kolkata";

          slots.push(slotSchema);
        } else {
          console.log(` Removing slot: ${slotStartTime} - ${slotEndTime} (Overlaps with break)`);
        }

        slotStart = slotEnd;
      }

      currentDate = currentDate.plus({ days: 1 });
    }

    if (slots.length > 0) {
      const result = await db.collection("SlotsDBSchema").insertMany(slots);
      res.status(201).json({
        message: "Slots created successfully (excluding holidays and breaks)",
        slots: result.insertedIds,
      });
    } else {
      res.status(200).json({ message: "No slots generated due to constraints." });
    }
  } catch (error) {
    console.error("Error creating slots:", error);
    res.status(500).json({ message: "Error creating slots", error });
  }
});

app.listen(port, () => {
  console.log(`🚀 Server running at http://localhost:${port}`);
});





const express = require("express");
const { MongoClient } = require("mongodb");
const cors = require("cors");
const { DateTime } = require("luxon");

const app = express();
const port = 5001;
const uri = "mongodb://localhost:27017";
const client = new MongoClient(uri);
const dbName = "createSlots";

app.use(cors());
app.use(express.json());

// Default Schema
function datas() {
  return {
    mainSchema: {
      interviewID: "",
      campaignID: "",
      roundNumber: 1,
      startDate: "",
      endDate: "",
      selected: false,
      deleted: false,
      event: "",
      allowJobseekerToReschedule: true,
      userID: "",
      resumeID: "",
      scheduledType: "",
      sourceOfBooking: [],
      availableMeetTypes: [],
      selectedMeetType: "",
      sourceOfDeletion: "",
      duration: 30,
      timeZone: "",
      timeZoneName: "",
      timeZoneFullName: "",
      sourceOfCreation: "Auto Fill",
      description: "",
      participants: [],
      location: {},
      phones: [],
      createdAt: "",
      createdBy: "",
      deletedAt: "",
      autoDelete: true,
      deletedBy: "",
      companyID: "",
      clientID: "",
    },
  };
}

app.post("/api/slots/", async (req, res) => {
  try {
    await client.connect();
    const db = client.db(dbName);
    const data = req.body.data;

    console.log(data.date, "Received holiday dates");

    let holidaySet = new Set();

    if (data.excludeHolidays) {
      data.date.forEach((holiday) => {
        let start = DateTime.fromISO(holiday.startDate).toISODate();
        let end = DateTime.fromISO(holiday.endDate).toISODate();

        let current = DateTime.fromISO(start);
        let endDate = DateTime.fromISO(end);

        while (current <= endDate) {
          holidaySet.add(current.toISODate());
          console.log(`🗓️ Adding Holiday: ${current.toISODate()}`);
          current = current.plus({ days: 1 });
        }
      });

      console.log(`Final Holiday Set:`, holidaySet);
    }

   
    let weekendSet = new Set();
    if (data.excludeWeekends && data.weekends) {
      data.weekends.forEach((weekendDay) => weekendSet.add(weekendDay));
      console.log(` Excluding Weekends:`, Array.from(weekendSet));
    }

    // Convert break periods to HH:mm format
    let breakPeriods = (data.time || []).map((breakHour) => ({
      start: DateTime.fromISO(breakHour.startime, { zone: "utc" })
        .setZone("Asia/Kolkata")
        .toFormat("HH:mm"),
      end: DateTime.fromISO(breakHour.endtime, { zone: "utc" })
        .setZone("Asia/Kolkata")
        .toFormat("HH:mm"),
    }));

    console.log(breakPeriods, "Break Periods (Only Time)");

    let startDate = DateTime.fromISO(data.startDate, { zone: "utc" }).setZone("Asia/Kolkata");
    let endDate = DateTime.fromISO(data.endDate, { zone: "utc" }).setZone("Asia/Kolkata");
    let duration = parseInt(data.duration.replace("min", ""), 10);
    let slots = [];
    let currentDate = startDate;

    while (currentDate <= endDate) {
      let formattedDate = currentDate.toFormat("yyyy-MM-dd");
      let weekdayName = currentDate.toFormat("EEEE");

     
      if (holidaySet.has(formattedDate)) {
        console.log(` Skipping ${formattedDate}, it's a holiday.`);
        currentDate = currentDate.plus({ days: 1 });
        continue;
      }

    
      if (weekendSet.has(weekdayName)) {
        console.log(` Skipping ${formattedDate}, it's a weekend (${weekdayName}).`);
        currentDate = currentDate.plus({ days: 1 });
        continue;
      }

      let workStart, workEnd;

      if (data.WeekFields && data.WeekFields.length > 0) {
        let daySchedule = data.WeekFields.find((item) => item[weekdayName]);

        if (daySchedule && daySchedule[weekdayName]) {
          let { startDate: startTime, endDate: endTime } = daySchedule[weekdayName];

          if (startTime && endTime) {
            workStart = DateTime.fromISO(startTime, { zone: "utc" })
              .setZone("Asia/Kolkata")
              .set({ year: currentDate.year, month: currentDate.month, day: currentDate.day });

            workEnd = DateTime.fromISO(endTime, { zone: "utc" })
              .setZone("Asia/Kolkata")
              .set({ year: currentDate.year, month: currentDate.month, day: currentDate.day });
          }
        }
      }

      if (!workStart || !workEnd) {
        console.warn(`⚠️ No working hours for ${weekdayName}. Defaulting to 9 AM - 6 PM.`);
        workStart = currentDate.set({ hour: 9, minute: 0 });
        workEnd = currentDate.set({ hour: 18, minute: 0 });
      }

      let slotStart = workStart;
      while (slotStart.plus({ minutes: duration }) <= workEnd) {
        let slotEnd = slotStart.plus({ minutes: duration });

        let slotStartTime = slotStart.toFormat("HH:mm");
        let slotEndTime = slotEnd.toFormat("HH:mm");

        let isBreakTime = breakPeriods.some((breakPeriod) => {
          let breakStartTime = breakPeriod.start;
          let breakEndTime = breakPeriod.end;

          return (
            (slotStartTime >= breakStartTime && slotStartTime < breakEndTime) ||
            (slotEndTime > breakStartTime && slotEndTime <= breakEndTime) ||
            (slotStartTime <= breakStartTime && slotEndTime >= breakEndTime)
          );
        });

        if (!isBreakTime) {
          let slotSchema = { ...datas().mainSchema };
          slotSchema.startDate = slotStart.toISO();
          slotSchema.endDate = slotEnd.toISO();
          slotSchema.duration = duration;
          slotSchema.description = data.description || "";
          slotSchema.timeZone = "Asia/Kolkata";

          slots.push(slotSchema);
        } else {
          console.log(` Removing slot: ${slotStartTime} - ${slotEndTime} (Overlaps with break)`);
        }

        slotStart = slotEnd;
      }

      currentDate = currentDate.plus({ days: 1 });
    }

    if (slots.length > 0) {
      const result = await db.collection("SlotsDBSchema").insertMany(slots);
      res.status(201).json({
        message: "Slots created successfully (excluding weekends, holidays, and breaks)",
        slots: result.insertedIds,
      });
    } else {
      res.status(200).json({ message: "No slots generated due to constraints." });
    }
  } catch (error) {
    console.error("Error creating slots:", error);
    res.status(500).json({ message: "Error creating slots", error });
  }
});

app.listen(port, () => {
  console.log(`🚀 Server running at http://localhost:${port}`);
});



























const express = require("express");
const { MongoClient } = require("mongodb");
const cors = require("cors");
const { DateTime } = require("luxon");

const app = express();
const port = 5001;
const uri = "mongodb://localhost:27017";
const client = new MongoClient(uri);
const dbName = "createSlots";

app.use(cors());
app.use(express.json());

// Default Schema
function datas() {
  return {
    mainSchema: {
      interviewID: "",
      campaignID: "",
      roundNumber: 1,
      startDate: "",
      endDate: "",
      selected: false,
      deleted: false,
      event: "",
      allowJobseekerToReschedule: true,
      userID: "",
      resumeID: "",
      scheduledType: "",
      sourceOfBooking: [],
      availableMeetTypes: [],
      selectedMeetType: "",
      sourceOfDeletion: "",
      duration: 30,
      timeZone: "",
      timeZoneName: "",
      timeZoneFullName: "",
      sourceOfCreation: "Auto Fill",
      description: "",
      participants: [],
      location: {},
      phones: [],
      createdAt: "",
      createdBy: "",
      deletedAt: "",
      autoDelete: true,
      deletedBy: "",
      companyID: "",
      clientID: "",
    },
  };
}

app.post("/api/slots/", async (req, res) => {
  try {
    await client.connect();
    const db = client.db(dbName);
    const data = req.body.data;

    console.log("Received Data:", JSON.stringify(data, null, 2));

    let holidaySet = new Set();
    if (data.excludeHolidays) {
      data.date.forEach((holiday) => {
        let start = DateTime.fromISO(holiday.startDate).toJSDate();
        let end = DateTime.fromISO(holiday.endDate).toJSDate();
        let current = DateTime.fromISO(start);
        let endDate = DateTime.fromISO(end);

        while (current <= endDate) {
          holidaySet.add(current.toJSDate());
          console.log(`🗓️ Adding Holiday: ${current.toJSDate()}`);
          current = current.plus({ days: 1 });
        }
      });
      console.log(`Final Holiday Set:`, holidaySet);
    }

    let weekendSet = new Set();
    if (data.excludeWeekends && data.weekends) {
      data.weekends.forEach((weekendDay) => weekendSet.add(weekendDay));
      console.log(`Excluding Weekends:`, Array.from(weekendSet));
    }

    let breakPeriods = (data.time || []).map((breakHour) => ({
      start: DateTime.fromISO(breakHour.startime, { zone: "utc" })
        .setZone("Asia/Kolkata")
        .toFormat("HH:mm"),
      end: DateTime.fromISO(breakHour.endtime, { zone: "utc" })
        .setZone("Asia/Kolkata")
        .toFormat("HH:mm"),
    }));
    console.log("Break Periods:", breakPeriods);

    let startDate = DateTime.fromISO(data.startDate, { zone: "utc" }).setZone("Asia/Kolkata");
    let endDate = DateTime.fromISO(data.endDate, { zone: "utc" }).setZone("Asia/Kolkata");
    let duration = parseInt(data.duration.replace("min", ""), 10);
    let slots = [];
    let currentDate = startDate;

    while (currentDate <= endDate) {
      let formattedDate = currentDate.toFormat("yyyy-MM-dd");
      let weekdayName = currentDate.toFormat("EEEE");

      if (holidaySet.has(formattedDate)) {
        console.log(`Skipping ${formattedDate}, it's a holiday.`);
        currentDate = currentDate.plus({ days: 1 });
        continue;
      }

      if (weekendSet.has(weekdayName)) {
        console.log(`Skipping ${formattedDate}, it's a weekend (${weekdayName}).`);
        currentDate = currentDate.plus({ days: 1 });
        continue;
      }

      let workStart, workEnd;

      console.log(`Checking working hours for ${weekdayName}`);
      if (data.WeekFields && data.WeekFields.length > 0) {
        let daySchedule = data.WeekFields.find((item) => Object.keys(item)[0] === weekdayName);

        if (daySchedule && daySchedule[weekdayName]) {
          let { startDate: startTime, endDate: endTime } = daySchedule[weekdayName];

          if (startTime && endTime) {
            workStart = DateTime.fromISO(startTime, { zone: "utc" })
              .setZone("Asia/Kolkata")
              .set({ year: currentDate.year, month: currentDate.month, day: currentDate.day });

            workEnd = DateTime.fromISO(endTime, { zone: "utc" })
              .setZone("Asia/Kolkata")
              .set({ year: currentDate.year, month: currentDate.month, day: currentDate.day });

            console.log(`✅ Found working hours for ${weekdayName}: ${workStart.toFormat("HH:mm")} - ${workEnd.toFormat("HH:mm")}`);
          }
        }
      }

      if (!workStart || !workEnd) {
        console.warn(`⚠️ No working hours found for ${weekdayName}. Skipping slots for this day.`);
        currentDate = currentDate.plus({ days: 1 });
        continue;
      }

      let slotStart = workStart;
      while (slotStart.plus({ minutes: duration }) <= workEnd) {
        let slotEnd = slotStart.plus({ minutes: duration });

        let slotStartTime = slotStart.toFormat("HH:mm");
        let slotEndTime = slotEnd.toFormat("HH:mm");

        let isBreakTime = breakPeriods.some((breakPeriod) => {
          return (
            (slotStartTime >= breakPeriod.start && slotStartTime < breakPeriod.end) ||
            (slotEndTime > breakPeriod.start && slotEndTime <= breakPeriod.end) ||
            (slotStartTime <= breakPeriod.start && slotEndTime >= breakPeriod.end)
          );
        });

        if (!isBreakTime) {
          let slotSchema = { ...datas().mainSchema };
          slotSchema.startDate = slotStart.toUTC().toISO();
          slotSchema.endDate = slotEnd.toUTC().toISO();
          slotSchema.duration = duration;
          slotSchema.description = data.description || "";
          slotSchema.timeZone = "Asia/Kolkata";

          slots.push(slotSchema);
        } else {
          console.log(`⏳ Removing slot: ${slotStartTime} - ${slotEndTime} (Overlaps with break)`);
        }

        slotStart = slotEnd;
      }

      currentDate = currentDate.plus({ days: 1 });
    }

    if (slots.length > 0) {
      const result = await db.collection("SlotsDBSchema").insertMany(slots);
      res.status(201).json({
        message: "Slots created successfully (excluding weekends, holidays, and breaks)",
        slots: result.insertedIds,
      });
    } else {
      res.status(200).json({ message: "No slots generated due to constraints." });
    }
  } catch (error) {
    console.error(" Error creating slots:", error);
    res.status(500).json({ message: "Error creating slots", error });
  }
});

app.listen(port, () => {
  console.log(`🚀 Server running at http://localhost:${port}`);
});















const express = require("express");
const { MongoClient } = require("mongodb");
const cors = require("cors");
const { DateTime } = require("luxon");

const app = express();
const port = 5001;
const uri = "mongodb://localhost:27017";
const client = new MongoClient(uri);
const dbName = "createSlots";

app.use(cors());
app.use(express.json());

// Default Schema
function datas() {
  return {
    mainSchema: {
      interviewID: "",
      campaignID: "",
      roundNumber: 1,
      startDate: "",
      endDate: "",
      selected: false,
      deleted: false,
      event: "",
      allowJobseekerToReschedule: true,
      userID: "",
      resumeID: "",
      scheduledType: "",
      sourceOfBooking: [],
      availableMeetTypes: [],
      selectedMeetType: "",
      sourceOfDeletion: "",
      duration: 30,
      timeZone: "",
      timeZoneName: "",
      timeZoneFullName: "",
      sourceOfCreation: "Auto Fill",
      description: "",
      participants: [],
      location: {},
      phones: [],
      createdAt: "",
      createdBy: "",
      deletedAt: "",
      autoDelete: true,
      deletedBy: "",
      companyID: "",
      clientID: "",
    },
  };
}

app.post("/api/slots/", async (req, res) => {
  try {
    await client.connect();
    const db = client.db(dbName);
    const data = req.body.data;

    console.log("Received Data:", JSON.stringify(data, null, 2));

    let holidaySet = new Set();
    if (data.excludeHolidays) {
      data.date.forEach((holiday) => {
        let start = DateTime.fromISO(holiday.startDate).toJSDate();
        let end = DateTime.fromISO(holiday.endDate).toJSDate();
        let current = DateTime.fromISO(start);
        let endDate = DateTime.fromISO(end);

        while (current <= endDate) {
          holidaySet.add(current.toJSDate());
          console.log(`🗓️ Adding Holiday: ${current.toJSDate()}`);
          current = current.plus({ days: 1 });
        }
      });
      console.log(`Final Holiday Set:`, holidaySet);
    }

    let weekendSet = new Set();
    if (data.excludeWeekends && data.weekends) {
      data.weekends.forEach((weekendDay) => weekendSet.add(weekendDay));
      console.log(`Excluding Weekends:`, Array.from(weekendSet));
    }

    let breakPeriods = (data.time || []).map((breakHour) => ({
      start: DateTime.fromISO(breakHour.startime, { zone: "utc" })
        .setZone("Asia/Kolkata")
        .toFormat("HH:mm"),
      end: DateTime.fromISO(breakHour.endtime, { zone: "utc" })
        .setZone("Asia/Kolkata")
        .toFormat("HH:mm"),
    }));
    console.log("Break Periods:", breakPeriods);

    let startDate = DateTime.fromISO(data.startDate, { zone: "utc" }).setZone(
      "Asia/Kolkata"
    );
    let endDate = DateTime.fromISO(data.endDate, { zone: "utc" }).setZone(
      "Asia/Kolkata"
    );
    let duration = parseInt(data.duration.replace("min", ""), 10);
    let slots = [];
    let currentDate = startDate;

    

    while (currentDate <= endDate) {
      let formattedDate = currentDate.toFormat("yyyy-MM-dd");
      let weekdayName = currentDate.toFormat("EEEE");

      if (holidaySet.has(formattedDate)) {
        console.log(`Skipping ${formattedDate}, it's a holiday.`);
        currentDate = currentDate.plus({ days: 1 });
        continue;
      }

      if (weekendSet.has(weekdayName)) {
        console.log(
          `Skipping ${formattedDate}, it's a weekend (${weekdayName}).`
        );
        currentDate = currentDate.plus({ days: 1 });
        continue;
      }

      let workStart, workEnd;

      console.log(`Checking working hours for ${weekdayName}`);
      if (data.WeekFields && data.WeekFields.length > 0) {
        let daySchedule = data.WeekFields.find(
          (item) => Object.keys(item)[0] === weekdayName
        );

        if (daySchedule && daySchedule[weekdayName]) {
          let { startDate: startTime, endDate: endTime } =
            daySchedule[weekdayName];

          if (startTime && endTime) {
            workStart = DateTime.fromISO(startTime, { zone: "utc" })
              .setZone("Asia/Kolkata")
              .set({
                year: currentDate.year,
                month: currentDate.month,
                day: currentDate.day,
              });

            workEnd = DateTime.fromISO(endTime, { zone: "utc" })
              .setZone("Asia/Kolkata")
              .set({
                year: currentDate.year,
                month: currentDate.month,
                day: currentDate.day,
              });

            console.log(
              `✅ Found working hours for ${weekdayName}: ${workStart.toFormat(
                "HH:mm"
              )} - ${workEnd.toFormat("HH:mm")}`
            );
          }
        }
      }

      if (!workStart || !workEnd) {
        console.warn(
          `⚠️ No working hours found for ${weekdayName}. Skipping slots for this day.`
        );
        currentDate = currentDate.plus({ days: 1 });
        continue;
      }

      let slotStart = workStart;
      while (slotStart.plus({ minutes: duration }) <= workEnd) {
        let slotEnd = slotStart.plus({ minutes: duration });

        let slotStartTime = slotStart.toFormat("HH:mm");
        let slotEndTime = slotEnd.toFormat("HH:mm");

        let isBreakTime = breakPeriods.some((breakPeriod) => {
          return (
            (slotStartTime >= breakPeriod.start &&
              slotStartTime < breakPeriod.end) ||
            (slotEndTime > breakPeriod.start &&
              slotEndTime <= breakPeriod.end) ||
            (slotStartTime <= breakPeriod.start &&
              slotEndTime >= breakPeriod.end)
          );
        });

        if (!isBreakTime) {
          let slotSchema = { ...datas().mainSchema };
          slotSchema.startDate = slotStart.toUTC().toISO();
          slotSchema.endDate = slotEnd.toUTC().toISO();
          slotSchema.duration = duration;
          slotSchema.description = data.description || "";
          slotSchema.timeZone = "Asia/Kolkata";

          slots.push(slotSchema);
        } else {
          console.log(
            `⏳ Removing slot: ${slotStartTime} - ${slotEndTime} (Overlaps with break)`
          );
        }

        slotStart = slotEnd;
      }

      currentDate = currentDate.plus({ days: 1 });
    }

    if (slots.length > 0) {
      const result = await db.collection("SlotsDBSchema").insertMany(slots);
      res.status(201).json({
        message:
          "Slots created successfully (excluding weekends, holidays, and breaks)",
        slots: result.insertedIds,
      });
    } else {
      res
        .status(200)
        .json({ message: "No slots generated due to constraints." });
    }
  } catch (error) {
    console.error(" Error creating slots:", error);
    res.status(500).json({ message: "Error creating slots", error });
  }
});

app.listen(port, () => {
  console.log(`🚀 Server running at http://localhost:${port}`);
});


















/// update holidays 













// const express = require("express");
// const { MongoClient } = require("mongodb");
// const cors = require("cors");
// const { DateTime } = require("luxon");

// const app = express();
// const port = 5001;
// const uri = "mongodb://localhost:27017";
// const client = new MongoClient(uri);
// const dbName = "createSlots";

// app.use(cors());
// app.use(express.json());

// // Default Schema
// function datas() {
//   return {
//     mainSchema: {
//       interviewID: "",
//       campaignID: "",
//       roundNumber: 1,
//       startDate: "",
//       endDate: "",
//       selected: false,
//       deleted: false,
//       event: "",
//       allowJobseekerToReschedule: true,
//       userID: "",
//       resumeID: "",
//       scheduledType: "",
//       sourceOfBooking: [],
//       availableMeetTypes: [],
//       selectedMeetType: "",
//       sourceOfDeletion: "",
//       duration: 30,
//       timeZone: "",
//       timeZoneName: "",
//       timeZoneFullName: "",
//       sourceOfCreation: "Auto Fill",
//       description: "",
//       participants: [],
//       location: {},
//       phones: [],
//       createdAt: "",
//       createdBy: "",
//       deletedAt: "",
//       autoDelete: true,
//       deletedBy: "",
//       companyID: "",
//       clientID: "",
//     },
//   };
// }

// // app.post("/api/slots/", async (req, res) => {
// //   try {
// //     await client.connect();
// //     const db = client.db(dbName);
// //     const data = req.body.data;

// //     console.log("Received Data:", JSON.stringify(data, null, 2));

// //     let holidaySet = new Set();
// //     if (data.excludeHolidays) {
// //       data.date.forEach((holiday) => {
// //         let start = DateTime.fromISO(holiday.startDate).toJSDate();
// //         let end = DateTime.fromISO(holiday.endDate).toJSDate();
// //         let current = DateTime.fromISO(start);
// //         let endDate = DateTime.fromISO(end);

// //         while (current <= endDate) {
// //           holidaySet.add(current.toJSDate());
// //           console.log(`🗓️ Adding Holiday: ${current.toJSDate()}`);
// //           current = current.plus({ days: 1 });
// //         }
// //       });
// //       console.log(`Final Holiday Set:`, holidaySet);
// //     }

// //     let weekendSet = new Set();
// //     if (data.excludeWeekends && data.weekends) {
// //       data.weekends.forEach((weekendDay) => weekendSet.add(weekendDay));
// //       console.log(`Excluding Weekends:`, Array.from(weekendSet));
// //     }

// //     let breakPeriods = (data.time || []).map((breakHour) => ({
// //       start: DateTime.fromISO(breakHour.startime, { zone: "utc" })
// //         .setZone("Asia/Kolkata")
// //         .toFormat("HH:mm"),
// //       end: DateTime.fromISO(breakHour.endtime, { zone: "utc" })
// //         .setZone("Asia/Kolkata")
// //         .toFormat("HH:mm"),
// //     }));
// //     console.log("Break Periods:", breakPeriods);

// //     let startDate = DateTime.fromISO(data.startDate, { zone: "utc" }).setZone(
// //       "Asia/Kolkata"
// //     );
// //     let endDate = DateTime.fromISO(data.endDate, { zone: "utc" }).setZone(
// //       "Asia/Kolkata"
// //     );
// //     let duration = parseInt(data.duration.replace("min", ""), 10);
// //     let slots = [];
// //     let currentDate = startDate;

    

// //     while (currentDate <= endDate) {
// //       let formattedDate = currentDate.toFormat("yyyy-MM-dd");
// //       let weekdayName = currentDate.toFormat("EEEE");

// //       if (holidaySet.has(formattedDate)) {
// //         console.log(`Skipping ${formattedDate}, it's a holiday.`);
// //         currentDate = currentDate.plus({ days: 1 });
// //         continue;
// //       }

// //       if (weekendSet.has(weekdayName)) {
// //         console.log(
// //           `Skipping ${formattedDate}, it's a weekend (${weekdayName}).`
// //         );
// //         currentDate = currentDate.plus({ days: 1 });
// //         continue;
// //       }

// //       let workStart, workEnd;

// //       console.log(`Checking working hours for ${weekdayName}`);
// //       if (data.WeekFields && data.WeekFields.length > 0) {
// //         let daySchedule = data.WeekFields.find(
// //           (item) => Object.keys(item)[0] === weekdayName
// //         );

// //         if (daySchedule && daySchedule[weekdayName]) {
// //           let { startDate: startTime, endDate: endTime } =
// //             daySchedule[weekdayName];

// //           if (startTime && endTime) {
// //             workStart = DateTime.fromISO(startTime, { zone: "utc" })
// //               .setZone("Asia/Kolkata")
// //               .set({
// //                 year: currentDate.year,
// //                 month: currentDate.month,
// //                 day: currentDate.day,
// //               });

// //             workEnd = DateTime.fromISO(endTime, { zone: "utc" })
// //               .setZone("Asia/Kolkata")
// //               .set({
// //                 year: currentDate.year,
// //                 month: currentDate.month,
// //                 day: currentDate.day,
// //               });

// //             console.log(
// //               `✅ Found working hours for ${weekdayName}: ${workStart.toFormat(
// //                 "HH:mm"
// //               )} - ${workEnd.toFormat("HH:mm")}`
// //             );
// //           }
// //         }
// //       }

// //       if (!workStart || !workEnd) {
// //         console.warn(
// //           `⚠️ No working hours found for ${weekdayName}. Skipping slots for this day.`
// //         );
// //         currentDate = currentDate.plus({ days: 1 });
// //         continue;
// //       }

// //       let slotStart = workStart;
// //       while (slotStart.plus({ minutes: duration }) <= workEnd) {
// //         let slotEnd = slotStart.plus({ minutes: duration });

// //         let slotStartTime = slotStart.toFormat("HH:mm");
// //         let slotEndTime = slotEnd.toFormat("HH:mm");

// //         let isBreakTime = breakPeriods.some((breakPeriod) => {
// //           return (
// //             (slotStartTime >= breakPeriod.start &&
// //               slotStartTime < breakPeriod.end) ||
// //             (slotEndTime > breakPeriod.start &&
// //               slotEndTime <= breakPeriod.end) ||
// //             (slotStartTime <= breakPeriod.start &&
// //               slotEndTime >= breakPeriod.end)
// //           );
// //         });

// //         if (!isBreakTime) {
// //           let slotSchema = { ...datas().mainSchema };
// //           slotSchema.startDate = slotStart.toUTC().toISO();
// //           slotSchema.endDate = slotEnd.toUTC().toISO();
// //           slotSchema.duration = duration;
// //           slotSchema.description = data.description || "";
// //           slotSchema.timeZone = "Asia/Kolkata";

// //           slots.push(slotSchema);
// //         } else {
// //           console.log(
// //             `⏳ Removing slot: ${slotStartTime} - ${slotEndTime} (Overlaps with break)`
// //           );
// //         }

// //         slotStart = slotEnd;
// //       }

// //       currentDate = currentDate.plus({ days: 1 });
// //     }

// //     if (slots.length > 0) {
// //       const result = await db.collection("SlotsDBSchema").insertMany(slots);
// //       res.status(201).json({
// //         message:
// //           "Slots created successfully (excluding weekends, holidays, and breaks)",
// //         slots: result.insertedIds,
// //       });
// //     } else {
// //       res
// //         .status(200)
// //         .json({ message: "No slots generated due to constraints." });
// //     }
// //   } catch (error) {
// //     console.error(" Error creating slots:", error);
// //     res.status(500).json({ message: "Error creating slots", error });
// //   }
// // });


// app.post("/api/slots/", async (req, res) => {
//   try {
//     await client.connect();
//     const db = client.db(dbName);
//     const data = req.body.data;

//     console.log("Received Data:", JSON.stringify(data, null, 2));

//     let holidaySet = new Set();
//     if (data.excludeHolidays) {
//       data.date.forEach((holiday) => {
//         let start = DateTime.fromISO(holiday.startDate).toISODate();
//         let end = DateTime.fromISO(holiday.endDate).toISODate();
//         let current = DateTime.fromISO(start);
//         let endDate = DateTime.fromISO(end);

//         while (current <= endDate) {
//           holidaySet.add(current.toISODate());
//           console.log(`🗓️ Adding Holiday: ${current.toISODate()}`);
//           current = current.plus({ days: 1 });
//         }
//       });
//       console.log(`Final Holiday Set:`, holidaySet);
//     }

//     let weekendSet = new Set();
//     if (data.excludeWeekends && data.weekends) {
//       data.weekends.forEach((weekendDay) => weekendSet.add(weekendDay));
//       console.log(`Excluding Weekends:`, Array.from(weekendSet));
//     }

//     let breakPeriods = (data.time || []).map((breakHour) => ({
//       start: DateTime.fromISO(breakHour.startime, { zone: "utc" })
//         .setZone("Asia/Kolkata")
//         .toFormat("HH:mm"),
//       end: DateTime.fromISO(breakHour.endtime, { zone: "utc" })
//         .setZone("Asia/Kolkata")
//         .toFormat("HH:mm"),
//     }));
//     console.log("Break Periods:", breakPeriods);

//     let startDate = DateTime.fromISO(data.startDate, { zone: "utc" }).setZone(
//       "Asia/Kolkata"
//     );
//     let endDate = DateTime.fromISO(data.endDate, { zone: "utc" }).setZone(
//       "Asia/Kolkata"
//     );
//     let duration = parseInt(data.duration.replace("min", ""), 10);
//     let slots = [];
//     let currentDate = startDate;

//     while (currentDate <= endDate) {
//       let formattedDate = currentDate.toISODate(); // Use ISO format
//       let weekdayName = currentDate.toFormat("EEEE");

//       if (holidaySet.has(formattedDate)) {
//         console.log(`Skipping ${formattedDate}, it's a holiday.`);
//         currentDate = currentDate.plus({ days: 1 });
//         continue;
//       }

//       if (weekendSet.has(weekdayName)) {
//         console.log(
//           `Skipping ${formattedDate}, it's a weekend (${weekdayName}).`
//         );
//         currentDate = currentDate.plus({ days: 1 });
//         continue;
//       }

//       let workStart, workEnd;

//       console.log(`Checking working hours for ${weekdayName}`);
//       if (data.WeekFields && data.WeekFields.length > 0) {
//         let daySchedule = data.WeekFields.find(
//           (item) => Object.keys(item)[0] === weekdayName
//         );

//         if (daySchedule && daySchedule[weekdayName]) {
//           let { startDate: startTime, endDate: endTime } =
//             daySchedule[weekdayName];

//           if (startTime && endTime) {
//             workStart = DateTime.fromISO(startTime, { zone: "utc" })
//               .setZone("Asia/Kolkata")
//               .set({
//                 year: currentDate.year,
//                 month: currentDate.month,
//                 day: currentDate.day,
//               });

//             workEnd = DateTime.fromISO(endTime, { zone: "utc" })
//               .setZone("Asia/Kolkata")
//               .set({
//                 year: currentDate.year,
//                 month: currentDate.month,
//                 day: currentDate.day,
//               });

//             console.log(
//               `✅ Found working hours for ${weekdayName}: ${workStart.toFormat(
//                 "HH:mm"
//               )} - ${workEnd.toFormat("HH:mm")}`
//             );
//           }
//         }
//       }

//       if (!workStart || !workEnd) {
//         console.warn(
//           `⚠️ No working hours found for ${weekdayName}. Skipping slots for this day.`
//         );
//         currentDate = currentDate.plus({ days: 1 });
//         continue;
//       }

//       let slotStart = workStart;
//       while (slotStart.plus({ minutes: duration }) <= workEnd) {
//         let slotEnd = slotStart.plus({ minutes: duration });

//         let slotStartTime = slotStart.toFormat("HH:mm");
//         let slotEndTime = slotEnd.toFormat("HH:mm");

//         let isBreakTime = breakPeriods.some((breakPeriod) => {
//           return (
//             (slotStartTime >= breakPeriod.start &&
//               slotStartTime < breakPeriod.end) ||
//             (slotEndTime > breakPeriod.start &&
//               slotEndTime <= breakPeriod.end) ||
//             (slotStartTime <= breakPeriod.start &&
//               slotEndTime >= breakPeriod.end)
//           );
//         });

//         if (!isBreakTime) {
//           let slotSchema = { ...datas().mainSchema };
//           slotSchema.startDate = slotStart.toUTC().toISO();
//           slotSchema.endDate = slotEnd.toUTC().toISO();
//           slotSchema.duration = duration;
//           slotSchema.description = data.description || "";
//           slotSchema.timeZone = "Asia/Kolkata";

//           slots.push(slotSchema);
//         } else {
//           console.log(
//             `⏳ Removing slot: ${slotStartTime} - ${slotEndTime} (Overlaps with break)`
//           );
//         }

//         slotStart = slotEnd;
//       }

//       currentDate = currentDate.plus({ days: 1 });
//     }

//     // ❗❗ Ensure that slots do not contain holiday slots before inserting into DB
//     slots = slots.filter(
//       (slot) => !holidaySet.has(DateTime.fromISO(slot.startDate).toISODate())
//     );

//     if (slots.length > 0) {
//       const result = await db.collection("SlotsDBSchema").insertMany(slots);
//       res.status(201).json({
//         message:
//           "Slots created successfully (excluding weekends, holidays, and breaks)",
//         slots: result.insertedIds,
//       });
//     } else {
//       res
//         .status(200)
//         .json({ message: "No slots generated due to constraints." });
//     }
//   } catch (error) {
//     console.error(" Error creating slots:", error);
//     res.status(500).json({ message: "Error creating slots", error });
//   }
// });

// app.listen(port, () => {
//   console.log(`🚀 Server running at http://localhost:${port}`);
// });


































const express = require("express");
const { MongoClient } = require("mongodb");
const cors = require("cors");
const { DateTime } = require("luxon");

const app = express();
const port = 5001;
const uri = "mongodb://localhost:27017";
const client = new MongoClient(uri);
const dbName = "createSlots";

app.use(cors());
app.use(express.json());

// Default Schema
function datas() {
  return {
    mainSchema: {
      interviewID: "",
      campaignID: "",
      roundNumber: 1,
      startDate: "",
      endDate: "",
      selected: false,
      deleted: false,
      event: "",
      allowJobseekerToReschedule: true,
      userID: "",
      resumeID: "",
      scheduledType: "",
      sourceOfBooking: [],
      availableMeetTypes: [],
      selectedMeetType: "",
      sourceOfDeletion: "",
      duration: 30,
      timeZone: "",
      timeZoneName: "",
      timeZoneFullName: "",
      sourceOfCreation: "Auto Fill",
      description: "",
      participants: [],
      location: {},
      phones: [],
      createdAt: "",
      createdBy: "",
      deletedAt: "",
      autoDelete: true,
      deletedBy: "",
      companyID: "",
      clientID: "",
    },
  };
}

app.post("/api/slots/", async (req, res) => {
  try {
    await client.connect();
    const db = client.db(dbName);
    const data = req.body.data;

    console.log(data.date, "Received holiday dates");

    let holidaySet = new Set();

    if (data.excludeHolidays) {
      data.date.forEach((holiday) => {
        let start = DateTime.fromISO(holiday.startDate).toISODate();
        let end = DateTime.fromISO(holiday.endDate).toISODate();

        let current = DateTime.fromISO(start);
        let endDate = DateTime.fromISO(end);

        while (current <= endDate) {
          holidaySet.add(current.toISODate());
          console.log(`🗓️ Adding Holiday: ${current.toISODate()}`);
          current = current.plus({ days: 1 });
        }
      });

      console.log(`🚫 Final Holiday Set:`, holidaySet);
    }

    // Handle weekends exclusion
    let weekendSet = new Set();
    if (data.excludeWeekends && data.weekends) {
      data.weekends.forEach((weekendDay) => weekendSet.add(weekendDay));
      console.log(`🚫 Excluding Weekends:`, Array.from(weekendSet));
    }

    // Convert break periods to HH:mm format
    let breakPeriods = (data.time || []).map((breakHour) => ({
      start: DateTime.fromISO(breakHour.startime, { zone: "utc" })
        .setZone("Asia/Kolkata")
        .toFormat("HH:mm"),
      end: DateTime.fromISO(breakHour.endtime, { zone: "utc" })
        .setZone("Asia/Kolkata")
        .toFormat("HH:mm"),
    }));

    console.log(breakPeriods, "Break Periods (Only Time)");

    let startDate = DateTime.fromISO(data.startDate, { zone: "utc" }).setZone("Asia/Kolkata");
    let endDate = DateTime.fromISO(data.endDate, { zone: "utc" }).setZone("Asia/Kolkata");
    let duration = parseInt(data.duration.replace("min", ""), 10);
    let slots = [];
    let currentDate = startDate;

    while (currentDate <= endDate) {
      let formattedDate = currentDate.toFormat("yyyy-MM-dd");
      let weekdayName = currentDate.toFormat("EEEE");

      // 🚫 Skip holidays
      if (holidaySet.has(formattedDate)) {
        console.log(`⛔ Skipping ${formattedDate}, it's a holiday.`);
        currentDate = currentDate.plus({ days: 1 });
        continue;
      }

      // 🚫 Skip weekends if specified
      if (weekendSet.has(weekdayName)) {
        console.log(`⛔ Skipping ${formattedDate}, it's a weekend (${weekdayName}).`);
        currentDate = currentDate.plus({ days: 1 });
        continue;
      }

      let workStart, workEnd;

      if (data.WeekFields && data.WeekFields.length > 0) {
        let daySchedule = data.WeekFields.find((item) => item[weekdayName]);

        if (daySchedule && daySchedule[weekdayName]) {
          let { startDate: startTime, endDate: endTime } = daySchedule[weekdayName];

          if (startTime && endTime) {
            workStart = DateTime.fromISO(startTime, { zone: "utc" })
              .setZone("Asia/Kolkata")
              .set({ year: currentDate.year, month: currentDate.month, day: currentDate.day });

            workEnd = DateTime.fromISO(endTime, { zone: "utc" })
              .setZone("Asia/Kolkata")
              .set({ year: currentDate.year, month: currentDate.month, day: currentDate.day });
          }
        }
      }

      if (!workStart || !workEnd) {
        console.warn(`⚠️ No working hours for ${weekdayName}. Defaulting to 9 AM - 6 PM.`);
        workStart = currentDate.set({ hour: 9, minute: 0 });
        workEnd = currentDate.set({ hour: 18, minute: 0 });
      }

      let slotStart = workStart;
      while (slotStart.plus({ minutes: duration }) <= workEnd) {
        let slotEnd = slotStart.plus({ minutes: duration });

        let slotStartTime = slotStart.toFormat("HH:mm");
        let slotEndTime = slotEnd.toFormat("HH:mm");

        let isBreakTime = breakPeriods.some((breakPeriod) => {
          let breakStartTime = breakPeriod.start;
          let breakEndTime = breakPeriod.end;

          return (
            (slotStartTime >= breakStartTime && slotStartTime < breakEndTime) ||
            (slotEndTime > breakStartTime && slotEndTime <= breakEndTime) ||
            (slotStartTime <= breakStartTime && slotEndTime >= breakEndTime)
          );
        });

        if (!isBreakTime) {
          let slotSchema = { ...datas().mainSchema };
          slotSchema.startDate = slotStart.toISO();
          slotSchema.endDate = slotEnd.toISO();
          slotSchema.duration = duration;
          slotSchema.description = data.description || "";
          slotSchema.timeZone = "Asia/Kolkata";

          slots.push(slotSchema);
        } else {
          console.log(` Removing slot: ${slotStartTime} - ${slotEndTime} (Overlaps with break)`);
        }

        slotStart = slotEnd;
      }

      currentDate = currentDate.plus({ days: 1 });
    }

    if (slots.length > 0) {
      const result = await db.collection("SlotsDBSchema").insertMany(slots);
      res.status(201).json({
        message: "Slots created successfully (excluding weekends, holidays, and breaks)",
        slots: result.insertedIds,
      });
    } else {
      res.status(200).json({ message: "No slots generated due to constraints." });
    }
  } catch (error) {
    console.error("Error creating slots:", error);
    res.status(500).json({ message: "Error creating slots", error });
  }
});

app.listen(port, () => {
  console.log(`🚀 Server running at http://localhost:${port}`);
});












///////////////final code holiday weekend  break 











const express = require("express");
const { MongoClient } = require("mongodb");
const cors = require("cors");
const { DateTime } = require("luxon");

const app = express();
const port = 5001;
const uri = "mongodb://localhost:27017";
const client = new MongoClient(uri);
const dbName = "createSlots";

app.use(cors());
app.use(express.json());

// Default Schema
function datas() {
  return {
    mainSchema: {
      interviewID: "",
      campaignID: "",
      roundNumber: 1,
      startDate: "",
      endDate: "",
      selected: false,
      deleted: false,
      event: "",
      allowJobseekerToReschedule: true,
      userID: "",
      resumeID: "",
      scheduledType: "",
      sourceOfBooking: [],
      availableMeetTypes: [],
      selectedMeetType: "",
      sourceOfDeletion: "",
      duration: 30,
      timeZone: "",
      timeZoneName: "",
      timeZoneFullName: "",
      sourceOfCreation: "Auto Fill",
      description: "",
      participants: [],
      location: {},
      phones: [],
      createdAt: "",
      createdBy: "",
      deletedAt: "",
      autoDelete: true,
      deletedBy: "",
      companyID: "",
      clientID: "",
    },
  };
}

app.post("/api/slots/", async (req, res) => {
  try {
    await client.connect();
    const db = client.db(dbName);
    const data = req.body.data;

    console.log(data.date, "Received holiday dates");

    let holidaySet = new Set();
    if (data.excludeHolidays) {
      data.date.forEach((holiday) => {
        let start = DateTime.fromISO(holiday.startDate).toISODate();
        let end = DateTime.fromISO(holiday.endDate).toISODate();

        let current = DateTime.fromISO(start);
        let endDate = DateTime.fromISO(end);

        while (current <= endDate) {
          holidaySet.add(current.toISODate());
          console.log(` Adding Holiday: ${current.toISODate()}`);
          current = current.plus({ days: 1 });
        }
      });

      console.log(`Final Holiday Set:`, holidaySet);
    }

    // Handle weekends exclusion
    let weekendSet = new Set();
    if (data.excludeWeekends && data.weekends) {
      data.weekends.forEach((weekendDay) => weekendSet.add(weekendDay));
      console.log(`🚫 Excluding Weekends:`, Array.from(weekendSet));
    }

    // Convert break periods to HH:mm format
    let breakPeriods = (data.time || []).map((breakHour) => ({
      start: DateTime.fromISO(breakHour.startime, { zone: "utc" })
        .setZone("Asia/Kolkata")
        .toFormat("HH:mm"),
      end: DateTime.fromISO(breakHour.endtime, { zone: "utc" })
        .setZone("Asia/Kolkata")
        .toFormat("HH:mm"),
    }));

    console.log(breakPeriods, "Break Periods (Only Time)");

    let startDate = DateTime.fromISO(data.startDate, { zone: "utc" }).setZone("Asia/Kolkata");
    let endDate = DateTime.fromISO(data.endDate, { zone: "utc" }).setZone("Asia/Kolkata");
    let duration = parseInt(data.duration.replace("min", ""), 10);
    let slots = [];
    let currentDate = startDate;

    //  Validate that working hours exist
    let hasWorkingHours = data.WeekFields && data.WeekFields.some((week) =>
      Object.values(week).some((schedule) => schedule.startDate && schedule.endDate)
    );

    if (!hasWorkingHours) {
      return res.status(400).json({
        message: "Slots are not created due to missing weekly working hours.",
      });
    }

    while (currentDate <= endDate) {
      let formattedDate = currentDate.toFormat("yyyy-MM-dd");
      let weekdayName = currentDate.toFormat("EEEE");

      //  Skip holidays
      if (holidaySet.has(formattedDate)) {
        console.log(`Skipping ${formattedDate}, it's a holiday.`);
        currentDate = currentDate.plus({ days: 1 });
        continue;
      }

      //  Skip weekends if specified
      if (weekendSet.has(weekdayName)) {
        console.log(`Skipping ${formattedDate}, it's a weekend (${weekdayName}).`);
        currentDate = currentDate.plus({ days: 1 });
        continue;
      }

      let workStart, workEnd;

      if (data.WeekFields && data.WeekFields.length > 0) {
        let daySchedule = data.WeekFields.find((item) => item[weekdayName]);

        if (daySchedule && daySchedule[weekdayName]) {
          let { startDate: startTime, endDate: endTime } = daySchedule[weekdayName];

          if (startTime && endTime) {
            workStart = DateTime.fromISO(startTime, { zone: "utc" })
              .setZone("Asia/Kolkata")
              .set({ year: currentDate.year, month: currentDate.month, day: currentDate.day });

            workEnd = DateTime.fromISO(endTime, { zone: "utc" })
              .setZone("Asia/Kolkata")
              .set({ year: currentDate.year, month: currentDate.month, day: currentDate.day });
          }
        }
      }

      if (!workStart || !workEnd) {
        console.log(`⚠️ No working hours for ${weekdayName}, skipping.`);
        currentDate = currentDate.plus({ days: 1 });
        continue;
      }

      let slotStart = workStart;
      while (slotStart.plus({ minutes: duration }) <= workEnd) {
        let slotEnd = slotStart.plus({ minutes: duration });

        let slotStartTime = slotStart.toFormat("HH:mm");
        let slotEndTime = slotEnd.toFormat("HH:mm");

        let isBreakTime = breakPeriods.some((breakPeriod) => {
          let breakStartTime = breakPeriod.start;
          let breakEndTime = breakPeriod.end;

          return (
            (slotStartTime >= breakStartTime && slotStartTime < breakEndTime) ||
            (slotEndTime > breakStartTime && slotEndTime <= breakEndTime) ||
            (slotStartTime <= breakStartTime && slotEndTime >= breakEndTime)
          );
        });

        if (!isBreakTime) {
          let slotSchema = { ...datas().mainSchema };
          slotSchema.startDate = slotStart.toISO();
          slotSchema.endDate = slotEnd.toISO();
          slotSchema.duration = duration;
          slotSchema.description = data.description || "";
          slotSchema.timeZone = "Asia/Kolkata";

          slots.push(slotSchema);
        } else {
          console.log(` Removing slot: ${slotStartTime} - ${slotEndTime} (Overlaps with break)`);
        }

        slotStart = slotEnd;
      }

      currentDate = currentDate.plus({ days: 1 });
    }

    if (slots.length > 0) {
      const result = await db.collection("SlotsDBSchema").insertMany(slots);
      res.status(201).json({
        message: "Slots created successfully ",
        slots: result.insertedIds,
      });
    } else {
      res.status(200).json({ message: "No slots generated due to constraints." });
    }
  } catch (error) {
    console.error("Error creating slots:", error);
    res.status(500).json({ message: "Error creating slots", error });
  }
});

app.listen(port, () => {
  console.log(`🚀 Server running at http://localhost:${port}`);
});
















final code








import { useCreateslotsMutation } from "./ApiSlice";
import { Modal, ButtonToolbar, Button } from "rsuite";
import { useState } from "react";
import "rsuite/dist/rsuite.min.css";
import Breaks from "./Breaks";
import { useForm, useFieldArray } from "react-hook-form";
import MyForm from "./FrontPart";
import Holidays from "./Footer";
import WeeklyHours from "./Weekly";
import Toast from "react-bootstrap/Toast";
import ToastContainer from "react-bootstrap/ToastContainer";

const SlotModal = () => {
  const [open, setOpen] = useState(false);
  const [size, setSize] = useState();
  const [showToast, setShowToast] = useState(false);
  const [toastMessage, setToastMessage] = useState("");
  const [toastVariant, setToastVariant] = useState("success");

  const handleOpen = (value) => {
    clearErrors();
    reset();
    setSize(value);
    setOpen(true);
  };

  const handleClose = () => setOpen(false);

  const {
    register,
    control,
    reset,
    clearErrors,
    handleSubmit,
    setError,
    watch,
    trigger,
    getValues,
    setValue,
    formState: { errors },
  } = useForm({
    defaultValues: {
      time: [{ startime: "", endtime: "" }],
    },
  });

  const { fields, append, remove } = useFieldArray({
    control,
    name: "time",
  });

  const { fields: fieldhollyday, append: hollydayappend, remove: removehollyday } = useFieldArray({
    control,
    name: "date",
  });

  const { fields: WeekFields, append: WeekAppend, remove: WeekRemove } = useFieldArray({
    control,
    name: "week",
  });

  const [updateSlot] = useCreateslotsMutation();

  const onSubmit = async (data) => {
    console.log(data);
    try {
      const response = await updateSlot({ data }).unwrap();
      setToastMessage(response.message);
      setToastVariant("success");
      setShowToast(true);                                                                 
      console.log("Update Response:", response);
    } catch (error) {
      setToastMessage("not weekly hours");
      setToastVariant("danger");
      setShowToast(true);
      console.error("no weekly hours:", error);
    }
  };

  return (
    <>
      <ButtonToolbar>
        <Button size="lg" onClick={() => handleOpen("calc(90% - 80px)")}>
          Create SlotModal
        </Button>
      </ButtonToolbar>

      <Modal size={size} open={open} onClose={handleClose}>
        <Modal.Header>
          <Modal.Title>Slots</Modal.Title>
        </Modal.Header>
        <Modal.Body>
          <form onSubmit={handleSubmit(onSubmit)}>
            <MyForm
              register={register}
              control={control}
              handleSubmit={handleSubmit}
              errors={errors}
              setError={setError}
              trigger={trigger}
              getValues={getValues}
              fields={fields}
              append={append}
              remove={remove}
              watch={watch}
              setValue={setValue}
            />

            <WeeklyHours
              register={register}
              errors={errors}
              reset={reset}
              setError={setError}
              clearErrors={clearErrors}
              trigger={trigger}
              getValues={getValues}
              watch={watch}
              setValue={setValue}
              WeekFields={WeekFields ?? []}
              WeekAppend={WeekAppend}
              WeekRemove={WeekRemove}
              control={control}
            />

            <Breaks
              register={register}
              control={control}
              handleSubmit={handleSubmit}
              errors={errors}
              setError={setError}
              trigger={trigger}
              getValues={getValues}
              fields={fields}
              append={append}
              remove={remove}
              watch={watch}
              setValue={setValue}
            />

            <Holidays
              register={register}
              errors={errors}
              setError={setError}
              trigger={trigger}
              getValues={getValues}
              watch={watch}
              setValue={setValue}
              fieldhollyday={
                fieldhollyday.length > 0
                  ? fieldhollyday
                  : [{ startDate: null, endDate: null, name: "" }]
              }
              hollydayappend={hollydayappend}
              removehollyday={removehollyday}
              control={control}
            />

            <div className="d-flex justify-content-center">
              <Button type="submit" appearance="primary">
                Prepare Slots
              </Button>
            </div>
          </form>
        </Modal.Body>
      </Modal>

      {/* Toast Notification */}
      <ToastContainer position="top-end" className="p-3" style={{ zIndex: 9999 }}>
        <Toast bg={toastVariant} show={showToast} onClose={() => setShowToast(false)} delay={3000} autohide>
          <Toast.Header>
            <strong className="me-auto">Notification</strong>
          </Toast.Header>
          <Toast.Body>{toastMessage}</Toast.Body>
        </Toast>
      </ToastContainer>
    </>
  );
};

export default SlotModal;
